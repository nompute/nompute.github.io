---
layout: post
title: Using Node.js cluster with logrotate
description: |
  I recently had occasion to convert an existing Node.js service for
  multiprocess use.  I opted to use Node's built-in "cluster" module, and
  realized that managing log files with log4js-node wasn't completely
  transparent.
---

# Using Node.js cluster with logrotate

I recently had occasion to convert an existing Node.js service for multiprocess
use.  I opted to use Node's built-in "cluster" module (we're running a recent
version of Node - the module disappeared for a release or two).

The trickiest part of the whole affair was dealing with log files.  We use
log4js-node, which has nice features like replacing console.log and also
allowing you to configure a myriad of different loggers.  Java programmers with
log4j experience would be right at home with the tool.

In theory, log4js-node has a server/client logger that was added precisely to
support processes using cluster.  However, it always seemed a little odd to
have what is essentially an operational concern be part of the code of the
service.  You could have different machines with different persistence
thresholds.  In that situation, you don't want to have to commit and deploy the
service when you could just edit a logrotate config file.

Most services have a nice way to tell them to reload their log file handles.
Apache will do this if you send SIGUSR1.  Node.js uses SIGUSR1 for debugging,
but SIGUSR2 is free.

This isn't particularly clean - log4js-node doesn't expose enough of its
internal handlers to be able to do this politely.  I basically took a hammer to
it and reloaded the entire logger config wholesale.  Below is an abstraction of
what it ended up looking like:

{% highlight js %}

if (cluster.isMaster) {
  // Listen for the signal
  process.on('SIGUSR2', function() {
    // Reload the logger configuration wholesale
    log4js.configure(LOG_CONFIG);
    // I'm actually not sure why this is required - I have replaceConsole
    // set to "true" in my configuration
    log4js.replaceConsole();

    for (var id in cluster.workers) {
      cluster.workers[id].send('reload_logs');
    }

    console.log("Log files reloaded.");
  });

  // Write the master PID into a tmp file (this is useful for logrotate so it
  // knows who to send SIGUSR2 to).
  fs = require('fs');
  fs.writeFile("/path/to/process.pid", process.pid);
}
else {
  process.on('message', function(msg) {
    if (msg === 'reload_logs') {
      log4js.configure(LOG_CONFIG);
      log4js.replaceConsole();
    }
  });
}

{% endhighlight %}

Finally, you'll want to add a line like this somewhere in your logrotate
configuration:

{% highlight js %}
postrotate "[ ! -f /path/to/process.pid ] || kill -USR2 `cat /path/to/process.pid`"
{% endhighlight %}

Voila!  Functional log rotation using the venerable logrotate tool, and
Node.js's cluster module.
