---
layout: post
title:  Fixes: search and abbreviations (5.0.17.3)
date:   2017-09-11
categories: jurism announcement
---

A [fresh release](https://juris-m.github.io/downloads) of the client
(ver. 5.0.17.3) is now available for manual installation. This is a bugfix
release, all users should install the new version.

The bugs addressed and the new behavior---plus a crowd-sourcing
invitation for legal abbreviation data---are described below.

## Search

In the initial release, variant fields were omitted from searches.
This release will search variants as well as main fields. The fix
may slow search performance slightly on large databases, but the
code can be optimized with a little effort. If you find searches to
be uncomfortably slow, post to the lists and I will take a look when
time permits.

## Abbreviations: the Court field

Changes to abbreviation support for legal references are as described
in a previous post. To recap, all legal-case references should include
a Court entry, and the Court entry should be set to the appropriate
form via the Abbreviation Filter, in the Institution Part listing.
In most citations, the Jurisdiction value will not appear directly,
but abbreviation of the Court name can the set to apply within a
specific jurisdiction.

Typing in the Court field will open a dropdown list of courts known
to exist within the selected jurisdiction. Selecting a court from
the list will set the value in the field. However, a bug in the initial
release of Juris-M 5.0 allowed *only* entries from the list---which
is a problem if the court you need to cite is not in it.

With this release, arbitrary text can be entered in the Court field.
Non-matching entries will be highlighted in yellow. (If a non-matching
entry is eventually added to Juris-M's internal lists, the yellow
highlight will disappear.)

## Abbreviations: crowdsourcing for law

The abbreviation conventions for citing legal resources are arcane and
detailed. For US law, the are fully described in the [Indigo
Book](https://law.resource.org/pub/us/code/blue/IndigoBook.html), a
publication of [Public.Resource.org](https://public.resource.org/).
The controlled lists for jurisdiction and court names make it possible
to automate the application of correct abbreviations in legal
citations.

Automation requires data, and the task matching abbreviations
specified in the Indigo Book to their respective Juris-M codes
is (straightforward but) time-consuming.

In the hope of soliciting a little help from our user community, I
have opened a Google Sheet containing all of the US jurisdiction/court
pairs currently known to Juris-M. I will post an editing link to
the Juris-M support lists shortly. Users should feel free to share
the link with anyone who might like to contribute.

Once the sheet is complete, I will grind the data into the
machine-readable form expected by Juris-M, and add it to the
standard abbreviation lists bundled with the Abbreviation Filter.

FB
