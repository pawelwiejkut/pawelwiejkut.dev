---
title: "Change transport description after release"
date: 2022-01-06T12:23:54+01:00
tags: ["ABAP","Hacks"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

If you are forced to change transport description after release, you have to consider following changes:

1. Use RDDIT076 to change the description - if not possible, you have to find a way to edit E07T and E070.

2. Change description in TMSBUFTXT to correct display of shorttext in STMS.