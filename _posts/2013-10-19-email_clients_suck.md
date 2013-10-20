---
layout: post
title: Email Clients Suck
description: |
  I recently had occasion to take a whirlwind tour through 5 different mail
  clients/services.  I ventured out into this desolate wasteland and returned a
  broken man.  Read about my journey.
---

# No, I'm not kidding.

Some time ago I had occasion, nay, the need to find an alternative to GMail's
wonderful email interface.  No, it had nothing to do with Snowden/CIA leaks or
the fear that someone was spying on my correspondences.  Along the way, I
experimented with Yahoo Mail, Microsoft Exchange on the Mac, Apple Mail,
Airmail, and mutt.

You know what? They all kind of suck.  Maybe I've been too trained by GMail's
paradigms, to be able to "tag" emails as opposed to filing them away into
folders.  Or the ability to do almost everything with keyboard shortcuts (this
is perhaps the biggest time saver for me), and find anything with an expressive
search language.

# Yahoo Mail

Let's start with Yahoo Mail.  This venerable email service has been around for
years.  I still know former colleagues who swear by their @yahoo.com email
addresses.  Recently, Yahoo refreshed their Mail product, and I believe it's
generally better for it.

The old version had these annoying tabs.  Which, if the internet is to be
believed, people _loved_.  OK, you're entitled to your own opinion.  But the
keyboard shortcuts...dear god.  _Arrow_ keys? I mean, they're (mostly) there,
but they're really annoying.  I'm an ardent vim user, but even emacs-style
shortcuts would be an improvement here.

They _finally_ added conversations.  Now, tabs + conversations could be a neat
feature differentiator from GMail, and I can see that being useful.

# Microsoft Exchange

Eww.  Terrible keyboard shortcuts (or flat-out non-existent ones), an
excessively spammy notification system, and massive bloat.  Oh yeah, one time
it asked if I wanted to update Microsoft Office.  I said yes.  IT CLOSED ALL MY
BROWSERS.  WHAT.

# Airmail

I'll be honest here.  I don't understand the hype.  Maybe all this is invalid,
because I was testing with a beta version.  I leapt for joy at the mention of
GMail-style keyboard shortcuts.  I had such high hopes for you, Airmail.  But
those shortcuts?  They don't work quite right.  Jump to the search bar, type
something in, hit enter.  Search results show up.  But your keyboard focus is
_still_ in the search bar.  How do you jump out?  Honestly, Airmail is quite
nice, but wasn't quite what I wanted.  I'm willing to keep an eye on it.

# mutt

Old faithful.  I spent a good few weeks on mutt, to force myself to learn to
use it.  The old Unix tools were never that user-friendly, but certainly
powerful.  Setup took hours, and for the most part I was following [Steve Losh's
excellent guide](http://stevelosh.com/blog/2012/10/the-homely-mutt/).

I got a kick out of composing emails on the terminal with vim, or piping HTML
emails through lynx.  But there are a few problems with that.  If you ever have to
deal with corporate email users, "inline" responses with highlights are fairly
commonplace.  Status reports in graph form are visually easy to digest.
Neither of those come across really well via text, and jumping into a browser
to view them felt like a jarring context switch.

I really wanted to like mutt.  I still dream of a modern mutt, with modern GUI
elements.  These were some of the bigger annoyances, for me:

- Fixed-width fonts aren't great for a lot of reading.  Fonts, colors, bold
  text, etc. all help guide the eye, and I felt as if I had a harder time
  absorbing what I was reading.
- No asynchronous actions.  With my flakey mail server, having msmtp hang for
  30 seconds was just painful.
- You don't see your replies threaded together, unless you copy an email into
  the inbox.  It's nice to refer to something I've already said.  I could find
  things pretty quickly with notmuch, but eh.
- On the subject of notmuch, while it's pretty fast, it's not
  near-instantaneous, like it is with any of the other email clients listed
  thus far.

And so, finally, I caved to the fact that I'm just not that 1337 and put mutt
usage on hold for the time being.

# Apple Mail (or what I'm unhappily using now)

Blazing fast search, a pleasant UI, easy connection with an Exchange server (as
you might've guessed, considering I mentioned Exchange/Outlook above).  BUT,
keyboard shortcut support is terrible.  Amazingly, there's a shortcut for
attaching a file (which GMail surpisingly lacks).  Unfortunately, Mail.app
insists on adding an icon, or even a preview of the attached item inline.  It's
really distracting when composing email.

But ultimately, I liked enough of what I saw (and the fact that it's native to
all Macs helps) that I tried to fix the shortcut issue.  Enter
[GMailinator](http://github.com/nompute/GMailinator)!  It's far from complete,
and I'd love for people to contribute and submit pull requests, but it already
makes working with Mail.app much, much better.

# But seriously...

If your email workflow isn't as heavily keyboard-driven, you may not take issue
with most of these email clients.  I admittedly had very specific criteria.
I'd definitely keep an eye out for Airmail, and perhaps Yahoo Mail.  There are
also other self-hosted webmail clients out there.
[Mailpile](http://www.mailpile.is) recently ran a successful Kickstarter
campaign, and product looks like it'll be gorgeous.  Finally,
if someone wants to take another stab at converting me to mutt, I'd be more
than happy to entertain them.
