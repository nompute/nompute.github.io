---
layout: layout
---

# Michael Lai

  I craft software for a living in sunny California.  I came here from
Singapore, by way of [Chicago](http://uchicago.edu).  When I'm not writing code,
I'm usually at wushu or enjoying the occasional game of StarCraft II.

  I currently work at [Lexity](http://lexity.com), building [cool
stuff](http://commercecentral.lexity.com), and naming components nonsensical
things.  You can also read about some of the [other things](/cv) I've done.

# Musings

<ul class="post-listing">
  {% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%B %e, %Y" }}</span>
  </li>
  {% endfor %}
</ul>
