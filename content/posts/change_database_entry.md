---
title: "Change any database entry in SE11/SE16"
date: 2018-02-11T20:44:24+02:00
tags: ["ABAP","hack","authorization","debugger"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Hi all,

Today I show you a very simple and short solution to add, edit or remove table entries by SE16. Sometimes you just want to just add a record to make some fast test, and there is no reason to make a maintenance view or write a program. There is a youtube video and text version, you can pick one which suits you more.

<iframe width="560" height="315" src="https://www.youtube.com/embed/evxRzGTY5lE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

1. First step to do this you just can go to SE16 select a table and run debug by insert /hs.
<img src="/change_database_entry/1.png" width="80%" />

2. Next, select i.e. „show record” option, and go to Breakpoints-> Breakpoint at-> Breakpoint at Subroutine.
<img src="/change_database_entry/2.png" width="80%" />

3. Program: SAPLSETB , Fmla: SET_STATUS_VAL . Press F8.
<img src="/change_database_entry/3.png" width="80%" />

4. Now change 'code’ value to one from „if” list, i.e EDIT if you want to edit the entry.
Violla, now you should be able to change and save entry.
<img src="/change_database_entry/4.png" width="80%" />


