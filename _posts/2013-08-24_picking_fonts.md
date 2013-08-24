---
layout: post
title: Picking Fonts
description: |
  Having not been completely satisfied with my font choices, I spent hours
  playing with font combinations before finally settling on Oswald for article
  headers, and Droid Serif for the article body.  Along the way I learned some
  interesting things about the differences in font rendering between Windows
  and OS X.
---
# Picking Fonts

Picking fonts is a massive rabbit hole.  The pickier you are with your
aesthetic, the deeper it gets.  Worse still if you're not really inducted into
the legions of typographical luminaries, with their intimate knowledge of
kerning and x-heights and serifs.  I wasn't satisfied with my previous
combination of Quicksand and Open Sans, and wanted to change it up.  I've also
been rather enamored of the font choices on Medium of late.  There's a bit of an
old-school charm to using serifs on the web.  For longer-form articles, I much
prefer having serifs.  Then again, I'd also wear a pocket watch if I could find
one I liked, so use that as your baseline of trust.  Charged with some
inspiration, I dived headlong into yet another frivolous expenditure of my free
time.

## To Serif, Or Non

The traditional wisdom is that serif fonts are better for reading, because they
guide the eyes.  They were, however, intended for physical type, at a much
higher resolution than what is possible on a computer display.  Sans-serif
fonts were simply cleaner at low resolutions, so for the most part, sans-serif
fonts came to dominate the internet.

But then technology happened, along with a design revolution of the internet.
More emphasis was placed on web-based typography, and computer font engines got
better and the font foundries started producing higher-quality fonts for the
screen.  Take a look at the most popular serifs on Google Fonts, and you'll
find that many of them are quite palatable.

After a couple of hours of mucking around, I thought I rather liked the
combination of Josefin Sans for headers, and Merriweather for body text.  On a
whim, I pulled up the site on my Windows desktop to do more A/B testing and was
horrified to see that Merriweather, quite frankly, looked terrible.

## Wherein I Waste More Time Learning About ClearType

*Why* did fonts on Windows look so bad?  Turns out, it's not entirely Windows'
fault.  ClearType's been around for a long time, and in comparison, ClearType
makes fonts look a little crisper than their Mac counterparts.  It also depends
much more on the quality of the font, relying on font hinting instructions to
improve the visual presentation of characters.  In contrast, OS X ignores
hinting and uses just subpixel anti-aliasing.

What OS X is doing works really well, apparently.  The baseline for fonts is
much better than in Windows.  But there's that Apple "I know better"
philosophy.  A part of me hates the fact that the font may be rendered in a
way that the designer did not intend.

## Closure

Armed with this information, I started A/B testing on both a Mac and Windows
box, and finally settled on Oswald for headers, and Droid Serif for body text.
PT Serif was a close contender, but I ultimately felt that Droid Serif worked
better at a larger range of font sizes than PT Serif, and decided to just go
with that.  Keep in mind that these are free fonts, though, and there is a
world of exceptional paid fonts, like Medium's FF Tisa Pro.

TL;DR - Test your fonts in Windows, too.  Oh, serifs and bowties are cool.
