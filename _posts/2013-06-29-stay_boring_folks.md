---
layout: post
title: Stay Boring, Folks
---

# Stay Boring, Folks

Startups are great - people who pick startups, I think, self-select for
environments that encourage use of bleeding-edge technology.  Many of the
people I meet are genuinely interested in the latest Javascript MVC/MVCC
framework, or that obscure new programming language.

Sometimes, I think the thrill-seekers in us tend to forget that the
tried-and-true have their merits, and ultimately, you're trying to build a
successful business.  Integrating buzzword tech for the sake of it just burdens
you with technical debt in the form of supporting nascent technology.

Spotify's article on [using "boring"
technology](http://labs.spotify.com/2013/02/25/in-praise-of-boring-technology/)
strikes me because of their extremely mature approach to engineering.  They
describe fairly well-established technology and use it to solve modern
problems, like dynamic service discovery.  Many of the problems young companies
face today are simply not that novel - your time is better spent on more
worthwhile pursuits.

The cost of integrating the new hotness isn't always apparent.  Let's take the
poster child of new-school programming hype, node.js, for example.  There's a
lot to love about node.js - it's pretty darn
[fast](http://www.techempower.com/benchmarks/), and uses the web's most popular
language.

However, when we first started using node.js, it didn't have a lot of common
libraries that you'd expect from more mature frameworks.
[Node-mysql](https://github.com/felixge/node-mysql), one of the most popular
node.js mysql connection libraries, didn't even have connection pooling then.
In fact, I ended up having to fix a [trivial
bug](https://github.com/Kijewski/node-mysql-pool/pull/1) before we could use
node-mysql-pool.

There were many other things that were lacking, and took time to build out -
logging to multiple streams, performance tuning, better stacktraces.  What you
gain by using new technology isn't always offset by the amount of learning you
need to do.

Don't get me wrong - learning for the sake of learning is great, and a necessity
for the industry.  However, unrationalized integration of a platform you don't
have good insight to could end up costing you time better spent on features that
will help your company succeed.

Part of maturing as an engineer is understanding what those trade-offs are.
However, it's also the job of good engineering management to be supportive of
experimentation where possible, because it makes your developers both happier
and better at their jobs.
