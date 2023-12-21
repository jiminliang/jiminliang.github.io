---
title: How to manage publications
date: 2023-12-18
image:
  focal_point: 'top'
---

How to manage the publication list

<!--more-->

Read the docs [Auto Import Publications](https://docs.hugoblox.com/tutorial/resume/step-3/)

(1) Prepare the publications.bib. 

The bib file shuld be named exactly the same as publications.bib. It will be uploaded to the github repository, but do not edit it inside the github workspace. Every time it is modified, you should delete the publications.bib in the repository and do the following steps again. 

(2) In the github codespace, delete the publications.bib if it is already there.

Sync the changes and wait until the actions in the repository are finished. 

(3) In the github repository, click Code -> Add file -> Upload files and upload the publications.bib. 

Wait until a new pull request shown in Pull requests.

(4) In the github repository, Pull requests -> confirm the pull request.

This will generate separate subfolds for each publication in \content\publication, each includes a cite.bib and an index.md.

Wait until the action is done.

(5) In the github codespace, sync the changes.

Please note: If you have imported a paper and a subfolder for that paper has been created, the paper's record in publications.bib will not be processed when you import publications.bib. If you want to update a paper, delete its subfolder before importing.