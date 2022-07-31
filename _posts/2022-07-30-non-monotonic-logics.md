---
layout: post
title:  "Non-Monotonic Logics"
date:   2022-07-30 12-19-00 +0200
categories: mathematics, logic, computer science
---

My master's thesis was on a database query language called Datalog. Usually, when a programmer thinks of a database, the kind of thing that comes to mind is a nicely indexed SQL table, or a bunch of documents in a MongoDB instance, or maybe even a GraphQL schema if you play with the hip kids. Instead, Datalog thinks of a database as a set of _ground facts_, which are basically just atomic statements like "_Meta is a company_" or "_Guy loves Roxy_", written like this:

$$ \textrm{ company(Meta) } \\ \textrm{ loves(Guy, Roxy) } $$

The equivalent of a schema for a Datalog database is a set of _rules_, which tells the database how the different ground facts are related. These rules can express things like "_if X is the mother of Y, then X is a woman_", or even constraints like "_there are no blue tigers_", which you could write like this:

$$ if~ \textrm{motherOf(X, Y)}, ~then~ \textrm{female(X)} \\ if~ \textrm{blue(X)} ~and~ \textrm{tiger(X)}, ~then~impossible~ $$

That last one is a funny way to write "_blue tigers are impossible_", but computers prefer it when everything is in the same format. Datalog query engines can take databases of ground facts and a set of rules and efficiently answer _queries_, which are questions like "_who is the mother of Thomas_" or "_list all cities that can be reached by road from Paris_":

$$ \textrm{motherOf(X, Thomas)}? $$

$$ if~ \textrm{connected(X, Y)}, ~then~ \textrm{reachable(X, Y)} \\ if~ \textrm{reachable(X, Y)} ~and~ \textrm{connected(Y, Z)}, ~then~ \textrm{reachable(X, Z)} \\ \textrm{reachable(Paris, X)}? $$

Different people write Datalog in different ways. Academics like to use symbols from mathematical logic to express this stuff, and production-grade implementations of Datalog (like [Datomic](https://docs.datomic.com/cloud/whatis/supported-ops.html#datalog)) usually have their own syntax for rules and queries. Personally I prefer the mathematical symbols, but I've gone with a weird English hybrid above to make things easier to read.

My thesis topic was extending Datalog to support _default rules_, which are a bit like the rules I've written above except they are only required to hold in _ordinary situations_. This is a bit vague, but one example that you are probably familiar with is the legal edict "_innocent until proven guilty_". This basically says that an accused is considered _innocent by default_, and it is only in the exceptional circumstance that evidence can be procured that we revoke the rule and considered them guilty:

$$ if~true, ~then~ \textrm{innocent(X)} \\ if~ \textrm{innocent(X)} ~and~ \textrm{crime(Y)}, ~then~by~default~not~ \textrm{evidenceFor(X, Y)} $$

It's an interesting research area mathematically, but I've been itching to do something more practical with it. At the moment I feel a bit like I'm building castles in my mind, so here's a brain dump of random, slightly more involved things to use or do with non-monotonic logics:

* Directly encode non-monotonic semantics in Z3 for rigorously exploring definitions? Or maybe do this in Coq or Lean, or some other proof-assistant? I'm quite fond of [Lean](https://leanprover-community.github.io/mathlib-overview.html) at the moment, as it has nice tooling, it's reasonably simple to understand and use, and it has a large library of existing mathematical concepts and theorems to branch off.

* Translate some part of the South African constitution into Defeasible Datalog as a proof-of-concept? As a non-expert, reading legal documents has always seemed suspiciously similar to reading mathematics or code to me. If there _are_ similarities, then it would be interesting to actually make a translation between the two domains.

* Discrete non-monotonic reasoning systems (like my Defeasible Datalog) have always felt a bit like hacky, analytic-philosophy-flavoured ways to do reasoning with uncertainty and exceptions to me. The gold standard for this is probability theory, and the fact that probability theory works can even be proven mathematically (see [Cox's theorem](https://en.wikipedia.org/wiki/Cox%27s_theorem), for instance). Can you actually express systems like Defeasible Datalog in terms of some kind of probabilistic system, such as Bayesian inference over an appropriate prior?
