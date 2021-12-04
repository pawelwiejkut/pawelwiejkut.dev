---
title: "Access transaction without auth"
date: 2017-12-16T21:44:24+02:00
tags: ["ABAP","Authorization","hack"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
How to access transaction without authorization ? One big requirement to do this trick is having to debug and replace function. Let’s start!

I prepared myself user without authorization to the db02 transaction. When I want to run this transaction, I get a message: „You are not authorized to use transaction”

<img src="/access_tcode_no_auth/1.png" width="80%" />

Go to the SE37 transaction, and display function module: AUTH_CHECK_TCODE.

<img src="/access_tcode_no_auth/2.png" width="80%" />

Now seat a breakpoint on line 28, when sy-subrc is checked.

<img src="/access_tcode_no_auth/3.png" width="80%" />

Double click on sy-subrc value, and change it to 0.

<img src="/access_tcode_no_auth/4.png" width="80%" />

Press F8, to continue the program. Now transaction should start normally.

<img src="/access_tcode_no_auth/5.png" width="80%" />
