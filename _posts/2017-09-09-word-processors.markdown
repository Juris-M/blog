---
layout: post
title:  "Word processor support"
date:   2017-09-07
categories: jurism announcement
---

To the consternation of many, Word integration support turned out to be
broken in the initial version of Juris-M 5.0. The bug was fixed in a
followup release (5.0.17.1), but an explanation is in order.

The underlying cause was quite simple. The source code of the
Standalone client inherited from Zotero contains a standard file of
descriptive data called `application.ini.` There is a value `name` in
this file, which I had changed from `Zotero` to `Jurism`. The macro
bundle inserted into Word for integration support relies on this value
to communicate with the client. When there is no application named
`Zotero`, the Word macro complains, and nothing works.

Fixing the bug was a simple matter of reverting the `name` value; but
the task of tracking down the problem alerted me to some complexity in
the Juris-M ecosystem that is no longer necessary.

In the Firefox ecosystem, plugins are identified by their unique
product ID. The word processor integration plugins maintained by the
Zotero team are configured to install only if Zotero (sniffed by its
ID) is also installed. Back in the very early days, when Juris-M was
called "Multilingual Zotero" (aka "MLZ"), I cheated on this system by
giving the "MLZ" plugin the same product ID as Zotero itself. As a
result, the Zotero word processor plugins worked just fine with my
hacked-up version of Zotero.

Move forward to 2015, when Firefox began requiring that plugins be
[submitted for
signing](https://blog.mozilla.org/addons/2015/02/10/extension-signing-safer-experience/)
by their maintainers. This was also around the time that MLZ was
relabeled as Juris-M. To satisfy the signing requirement, I had to give
Juris-M its own unique product ID; and when I did so, the Zotero word
processor integration plugins refused to install. In a house-that-Jack-built
domino effect, this forced me to rebundle the Zotero integration plugins
with Juris-M identifiers, and submit them separately for signing.
In addition to adding the ID, I changed the logo and made some other minor
changes, but the underlying code was Zotero-original all the way.

The signing procedures were intended to block malicious code from the
Firefox platform. In practice, they proved to be a considerable
headache to developers. The requirement was loosened after a
[rancorous
exchange](https://danstillman.com/2015/11/23/firefox-extension-scanning-is-security-theater)
between the development lead at Zotero and the Firefox team.  However,
the roadmap laid out by Firefox to address legitimate security
concerns with their plugin infrastructure promised to make
continuation of Zotero in that environment difficult. Accordingly, the
Zotero team have laid out a long-term plan to migrate to another
platform (Electron).

Now move further forward to 2017. From Firefox 55, Zotero will no
longer run as a browser plugin. As an interim solution, Zotero 5.0 and
Juris-M 5.0 standalone clients are being run on a pre-version-55 copy of
Firefox, with the browser elements stripped out, *and with the signing
requirement disabled by default*.

This brings us back to the original issue. Since the native Zotero
word processor integration plugins can communicate quite happily with
Juris-M, and since the signing requirement no long applies in the 5.0
Standalone clients, there is no longer a reason to maintain separate
copies of these plugins. I can use the native plugin code, inserting
only a tiny tweak to extend compatibility to Juris-M.

That is why, if you examine the list of Add-on extensions in Juris-M
5.0, you will see a bright shiny Zotero logo next to the integration
plugins---we're *finally* back to getting the full labor-saving
benefit of open source publication there.

And so at length our tale of a shaggy dog arrives at its felicitous
conclusion.

FB
