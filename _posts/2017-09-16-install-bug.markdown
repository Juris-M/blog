---
layout: post
title:  "Bug: installing over Zotero"
date:   2017-09-16
categories: jurism bug
---

We have encountered a bug locally that is triggered when Juris-M 5.0
is installed over an existing Zotero installation.

The bug raises an error complaining about failure to find a database
table `zlsPreferences`. Juris-M attempts to copy, then modify an
existing database. If the database it finds happens to be from Zotero,
this table does not exist, hence the error.

I am on the road until the 25th, and won't be able to fix this bug
until after I return to Nagoya. Meanwhile, though, you should be able
to work around the error by following steps like these (essentially,
the idea is to prevent Juris-M from finding the previous Zotero
database, so that it will install an empty one that can be populated
via sync):

1. Stop Juris-M, Zotero, and (just in case) Firefox.
2. Use Finder (on the Mac), Cortana/Search (on Windows),
   or`find'/`locate` (on Linux) to locate the file `zotero.sqlite`
3. Rename the folder containing `zotero.sqlite` to something else
   (ie. rename `zotero` to `zoteroX`, or `Zotero` to `ZoteroX`)
4. If you also find a `jurism.sqlite` file on the system, rename
   it to (for example) `jurism-errored.sqlite`.
5. Install Juris-M 5.0 (you should not get an error this time).
6. Set up sync
7. Sync

That should pull in all of the content. Check that the attachments
have also come through.

Hope this works well!

FB
