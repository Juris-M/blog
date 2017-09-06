---
layout: post
title:  "Where is my library?"
date:   2017-09-06
categories: jurism announcement
---

## The Issue

Some users have found that Juris-M 5.0 did not locate an existing
Zotero or Juris-M data directory automatically when installed, resulting
in an empty library. When this happens, the data has not been lost;
it is only necessary to point the client at the location of the original
library.

Do be sure that you have a good backup before making the adjustment. (Backups
are *always* important. If you don't have a habit of making a regular backup
of all your personal data, today is a good day to start.)

## Finding the Old Library

Use the search facility of your computer to find
the original data directory. 

![Finding Jurism](images/search-for-jurism.png)

If you installed Juris-M for the first time
on a Zotero system, the file to look for is named `zotero.sqlite`.  If
you have upgraded from an earlier version of Juris-M, look for a file
named `jurism.sqlite`. A Windows search is shown in the illustration.
Note that you can see its file address by rolling the cursor over it
in the search listing. (On a Mac you can use the Finder for the same
purpose.)

## Changing the Data Directory

In the Juris-M 5.0 client, change your library's data directory.

![Select a Data Directory](images/select-data-directory.png)

Visit `Preferences` ➜ `Advanced`, and
select the `Files and Folders` tab. Under "Data Directory Location"
select "Custom," and navigate the popup file manager to the directory
identified in the previous step.

When the new directory is selected in the file manager,
Juris-M will pop up a reminder that data files must be present
is the directory, and offer to quit "Zotero" (at present---obviously
this should read "Juris-M").

When "OK" is clicked, Juris-M wil shut down. When the client is
next restarted, the content of the selected library will be
visible.

This is the simplest method of restoring the previous library
content. An alternative method would be to rename the `Juris-M`
directory at the top of your home account, and move or copy the
previous data directory to that location.  This may be
preferred---particularly if the previous data is buried deep among in
the Firefox profile data area---but as it is somewhat more
complicated, and can be affected by disk capacity limits, that
method is not described in detail here.

--- Frank Bennett, Nagoya
