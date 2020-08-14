# Felt

Felt is a simple [story sifting](https://mkremins.github.io/publications/Felt_SimpleStorySifter.pdf) and simulation engine for emergent narrative play experiences. It provides narrative system developers with tools for defining _story sifting patterns_ that match narratively potent sequences of events, and for building simulations in which characters make use of story sifting to reason about the world.

For example, here's a Felt sifting pattern that captures a "violation of hospitality" microstory, in which a traveling character enters a town, is shown hospitality by a resident of this town, and then experiences harm at the hands of this same town resident character:

```edn
; match a sequence of three events...
(eventSequence ?e1 ?e2 ?e3)

; ...in which the first event involves a guest entering town...
[?e1 eventType enterTown] [?e1 actor ?guest]

; ...the second involves a resident of the town showing them hospitality...
[?e2 eventType showHospitality] [?e2 actor ?host] [?e2 target ?guest]

; ...the third involves the same resident harming the guest...
[?e3 tag harm] [?e3 actor ?host] [?e3 target ?guest]

; ...and in which the guest didn't leave town between the first and last "anchor" events
(not-join [?eMid]
  (eventSequence ?e1 ?eMid ?e3)
  [?eMid eventType leaveTown] [?eMid actor ?guest])
```

By providing emergent narrative systems with the capacity to identify and extract these kinds of evocative microstories from the "raw material" of [character-centric](https://www.cc.gatech.edu/~riedl/pubs/aiide08.pdf) narrative simulation, we hope to improve the ability of these systems to _understand_ the emergent stories they're creating—and, consequently, the effectiveness of these systems at collaborative storytelling with a human interactor.

This repository contains a provisional standalone version of Felt. So far, active Felt development has mostly taken place in a series of repositories for specific projects that make use of Felt, including [Why Are We Like This?](https://github.com/ItsProbablyFine/WAWLT) and [Diarytown](https://github.com/meldckn/diarytown-prototypes). For examples of how to define Felt sifting patterns or simulation domains, it's probably best to start with one of these repositories.

In addition to the `felt.js` file included here, you'll also need some version of [DataScript](https://github.com/tonsky/datascript) included in your project to work with Felt.

For more information about Felt, see the following publication:

* [Felt: A Simple Story Sifter](https://mkremins.github.io/publications/Felt_SimpleStorySifter.pdf). Max Kreminski, Melanie Dickinson, and Noah Wardrip-Fruin. International Conference on Interactive Digital Storytelling (ICIDS), 2019.
