---
title: How to manage publications
date: 2023-12-18
image:
  focal_point: 'top'
---

How to manage the publication list

<!--more-->

(1) Make sure the import-publications.yml is in .github/workflows/

(2) Create publications.bib in the main path and put BibTex records of the publications in it. 

(3) In the github repository, click Actions -> Import Publications from BibTex.

This will generate separate subfolds for each publication in \content\publication, each includes a cite.bib and an index.md.

(4) Click pages-build-deployment to publish the website.


