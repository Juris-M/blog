---
layout: post
title:  "Abbreviations: changes in version 5.0.17.2"
date:   2017-09-09
categories: jurism announcement
---

## Introduction

A fresh release of the client is up that introduces small but
significant changes to the handling of abbreviations. This note
explains what the changes are, and provides guidance on how to manage
a few common cases.

Abbreviation support is an important part of Juris-M's mission in the
legal sphere, in particular. As anyone who has glanced through the
[Indigo
Book](https://law.resource.org/pub/us/code/blue/IndigoBook.html) (or
the [Bluebook](https://www.legalbluebook.com/)) is painfully aware,
legal citation styles typically impose complex and detailed
abbreviation requirements on the author. The rules were developed
before the advent of office automation, and supporting them in
software is a daunting task, on a level with a modest expert system.

In Zotero, abbreviations are applied from a static list of commonly
accepted abbreviations. This is not adequate for legal writing, since
abbreviated forms may vary according to the jurisdiction being cited.
Apart from the complexity this introduces, the number of jurisdictions
on the planet is rather large, and Juris-M aims to offer reasonably
good support to all of them. To achieve that, editing support for
abbreviation lists is a must. The Abbreviation Filter plugin, bundled
with the Juris-M 5.0 client, was thus an early addition to the Juris-M
ecosystem. It is fair to say that abbreviation support has been the
least-stable feature of Juris-M over the years, as it covers entirely
novel ground. We have literally had to make things up as we have gone
along, and there have been speed bumps.

We again hit a speed bump in Juris-M 5.0 release, but with the
5.0.17.2 release, I am fairly confident that it will be the last
we experience for awhile.

## Abbreviation Filter overview

Access the Abbreviation Filter by clicking on the **Abbrevs** button
in the Style Editor (Preferences -> Cite -> Style Editor), or in
either of the word processor integration popups. Clicking on the
button opens the citation editing panel. Abbreviations are divided
into several categories. Switch between categories by clicking on the
button that spans the width of the popup.

The popup view shows only entries that *can* be abbreviated in the
current document, applying the currently selected style. It does not
provide access to the entire abbreviation list (as the list of
abbreviations can expand without limit, that would be overwhelming).

Under the category button, entries are made up of three elements,
divided into columns.

* The center column shows the match keys for abbreviations. Keys are
  shown in lowercase text. When the citation processor attempts to
  abbreviate text tagged with `form="short"` in the style, the
  content of the input field will also be forced to lowercase,
  for matching purposes.

* The left column shows one or more jurisdiction targets for each
  match key.  Every key has at least a `default` target. Legal
  references that specify a jurisdiction will also have one or more
  jurisdiction entries, beginning with a country-level jurisdiction,
  and incrementing up to the specific item jurisdiction(s) containing
  a match for the key in the input data.

* The right column is for the abbreviation text. To edit, add, or remove
  an abbreviation, click in the area to the right of a match key.
  The field will open for editing. Press the `Enter` key to save the field.

Choose a jurisdiction target according to the scope that would wish an
abbreviation to apply. A `default` entry will apply to any item field
of the given category that matches the key. To apply a US legal
abbreviation across all US materials, enter the abbreviation in the
`United States|US` entry, and leave any more-specific jurisdiction
targets blank.

Abbreviations are saved in a database, and persist between sessions
and across documents. They are tied to the currently selected style,
however. Separate citation styles can apply entirely different
abbreviation rules (or none at all).

**Note:** In the initial Juris-M 5.0 release, the Abbreviation Filter did not
force keys to lowercase for matching or storage purposes. Because the
4.0 version of the Filter *did* (properly) store keys in lowercase form,
no previously entered abbreviations were available after installation.
You should find that your past abbreviations wake up after installing
5.0.17.2.

## Import and export

At the bottom of the popup, there are buttons for use in importing and
exporting abbreviation lists. The broad button opens a pulldown list
of standard lists (note that data in the law-related lists are
currently somewhat out of date, and may not be very useful yet).
Click on the label to change the button to an input field with a
file picker, to select an external list for import (such as a list
exported from another style, or by another user). Note the three
input modes, which provide control over the effect of an import on
existing list content.

## Jurisdiction suppression

The most recently added feature of the Abbreviation Filter is the one
that appears at the top: jurisdiction suppression.  It was introduced
in the 4.0 version of the plugin following a suggestion by Dan Epps. I
made some changes to its behavior at the 5.0 threshold, and soon after
the release, Michael Risch pointed out that I had actually messed
things up.  At 5.0.17.2, I think we may finally have gotten this one
right.

Jurisdiction suppression affects only the rendered form when the
`jurisdiction` variable is directly printed. It does not affect
the variable as used for matching purposes. Several users have
raised a question over whether this variable ever needs to be printed
at all. I have been stubborn about it, for two independent reasons:

1. In comparative law writing (common among our students and faculty at
   Nagoya), there are times when the national jurisdiction needs to be
   indicated in citations; and
2. It may be necessary to specify the jurisdiction in detail when
   citing unreported cases.

That said, in many contexts, the jurisdiction information just gets
in the way, and the global suppression feature is meant to given
general control over whether to include it.

### Previous versions

In the 4.0 version of the plugin (if I recall correctly), all
"children" of the selected jurisdiction were suppressed
indiscriminately. This served the purpose of eliminating clutter, but
with the downside that it became awkward to produce citations of type
(2) above. In addition, in our local manuscripts with citations of
type (1), turning off suppression exposed excessive detail in many
citations.

In the first cut of 5.0, I adjusted the suppression logic to quash
only specific jurisdictions, leaving children exposed in the output.
This was clever enough, but on reflection it didn't cleanly satisfy
either type (1) or type (2) requirements above. Unnecessary clutter
would still be exposed in the former, and as the suppression levels
selected affected all citations in the document, it didn't address the
latter at all well either.

When Michael pointed out that the additional click-work needed in
writing of any complexity would be troublesome, I was forced to think
again about how best to satisfy the two requirements above.

### Current version

Jurisdiction information is passed through to the citation in two
ways: as *code* (used to select the style module and to match
abbreviation keys); and as a *variable* (rendered directly in the
citation in human-readable form).

As Michael reminded me after the 5.0 release, the latter is a rare
case in most writing. A citation element such as "1st Cir." may
describe a jurisdiction, but it is in fact a concise expression of
*court and jurisdiction* combined (i.e. "the Court of Appeal for the
First Circuit of the United States"). It is semantically equivalent to
"Court of Appeal" with the jurisdiction target of "US|First Circuit"
in the Abbreviation Filter popup, as found in the "Institution Part"
category. We get a correct citation by setting an abbreviation for
that value. There is no need to separately render jurisdiction
information. This is true in almost all cases.

For comparative law writing (type 1 above), it is actually only
necessary to indicate the top-level, national jurisdiction. To meet
that requirement without unnecessary clutter, I have added a
`jurisdiction-depth` attribute to the Juris-M version of the CSL
stylesheet language, and set `jurisdiction-depth="1"` everywhere
the variable is rendered in the existing modular styles. That will
yield a country name, which is all we need.

With that change in place, the search dropdown for suppression need
only show top-level jurisdiction names. In most cases, this will
entirely suppress the selected jurisdiction from rendered citations
(which attempt only to render the country name). When more detail is
required, as when citing an unreported case, the effect will be only
to snip off the top-level element of the jurisdiction description, so
these cites should also work as expected.

While I am fairly confident that we have at last hit the sweet spot
with this feature, there will undoubtedly be teething troubles.
If you run into difficult cases (so to speak), please post a note
to the support lists, and I will see what we can do to make things
easier.

FB
