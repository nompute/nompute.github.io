---
layout: layout
title: Tiling windows in Mac OS X with Slate
---

#Tiling windows in Mac OS X with Slate

I hate moving windows around.  I'm comfortable with a mouse and a keyboard,
often at the same time.  But I still hate having to move windows around.  I've
been looking for a way to replicate the functionality of tiling window managers
like [Awesome](http://awesome.naquadah.org), [dwm](http://dwm.suckless.org) and
[xmonad](http://xmonad.org) on the Mac for quite some time.

There have been quite a few tools over the years, like
[Divvy](http://mizage.com/divvy), but I'm cheap and kept holding out for free
alternatives.  [Spectacle](http://spectacleapp.com) was what I used for quite a
while, and over time most of the engineers in the office also adopted it.  It's
still not ideal, however, because windows need to be manually positioned, and
the presets are quite limited.

I should note that [xnomad](http://github.com/fjolnir/xnomad) was a notable
development, because it did succeed in replicating much of the behavior of Linux
tiling window managers.  However, it relied on a homegrown bastard child of
Objective-C and Ruby, and you need to have that installed before the application
works. I've a strong aversion to one-man language interfaces and additional
dependencies, so this was a no-go for me.

Around this time a coworker introduced me to
[Slate](http://github.com/jigish/slate).  I was originally turned off by the
need for extreme configuration, but after reading up a bit more, it turned out
to have a number of very promising features:

* JavaScript configuration
* Event hooks on window/application creation
* APIs for iterating over all applications/windows

There's really endless possibility here, and people have set up some very
complex layouts.  Slate's notion of a Layout is nice if you have a static
environment, but it won't automatically adapt to new applications.  However, the
configuration scheme does allow you to at least emulate automatic tiling.
Here's a basic tiling function:

{% highlight js %}
var retile = function(windowObject) {
  var windows = [];
  slate.eachApp(function(app) {
    app.eachWindow(function(win) {
      if (win.isMinimizedOrHidden()) return;
      if (null == win.title() || win.title() === "") return;
      windows.push(win);
    });
  });

  var ss          = s.rect();
  var windowSizeX = ss.width * 0.4;
  var windowSizeY = ss.height / (windows.length - 1);
  var winPosY     = 0;

  for (i = 0; i < windows.length; i++) {
    w = windows[i];

    if (w.title() == windowObject.title()) {
      mainWidth = (windows.length > 1) ? "screenSizeX*0.6" : "screenSizeX";

      w.doOperation("move", {
        "x": "screenOriginX",
        "y": "screenOriginY",
        "width": mainWidth,
        "height": "screenSizeY"
      });
    }
    else {
      w.doOperation("move", {
        "x": "screenSizeX*0.6",
        "y": winPosY,
        "width": windowSizeX,
        "height": windowSizeY
      });

      winPosY += windowSizeY;
    }
  }
}

// Basic keybinds
slate.bindAll({
  "f:cmd,alt": slate.op("move", {"x": "screenOriginX", "y": "screenOriginY",
    "width": "screenSizeX", "height": "screenSizeY"}),
  "left:cmd,alt": slate.op("push", {"direction": "left", "style":
    "bar-resize:screenSizeX/2"}),
  "right:cmd,alt": slate.op("push", {"direction": "right", "style":
    "bar-resize:screenSizeX/2"}),

  "r:cmd,alt": retile,
  "w:alt": slate.op("hint"),
});
{% endhighlight %}

Hitting Cmd+Opt+r will tile all windows on the current screen/space so that they
don't overlap.  A single window will be full-screened, and additional windows
will start to divide up the screen space.  I'm keeping the notion of a "master"
window from dwm/Awesome/scrotwm, and the way things work right now, the
currently focused window is promoted to the master.

Now, let's see about automatically calling the <code>retile</code> function on
window events.  Turns out, this is pretty simple:

{% highlight js %}
slate.on("windowOpened", function(event, win) { retile(win); });
slate.on("windowClosed", function(event, win) { retile(win); });
slate.on("appOpened", function(event, win) { retile(win); });
slate.on("appClosed", function(event, win) { retile(win); });
slate.on("appHidden", function(event, win) { retile(win); });
slate.on("appUnhidden", function(event, win) { retile(win); });
{% endhighlight %}

That's all there is to it, with a couple limitations. The Javascript API won't
let you inspect things like AXRole or AXSubrole in the Objective-C world, which
means you won't necessarily be able to distinguish between dialog boxes and
primary application windows.  Slate also isn't Spaces aware, which is a bit of a
problem for a virtual desktop junkie like me.

It's a great start, however, and if I get the chance I'll see about adding in
the hooks needed for even better tiling support.  Or, you could beat me to it.

Got any other suggestions for configuring Slate?  Hit me up on
[Twitter](http://twitter.com/nompute).
