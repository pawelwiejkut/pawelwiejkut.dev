---
title: "How to change any database entries in SE16 or SE11"
date: 2021-12-25T14:51:25+01:00
tags: ["SE16","SE11","Database","Authorization"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
Focus_Keyword: "change entry SE16"
Victor_Hugo: "true"
---

Sometimes we are forced to change some database entries. There are many reasons like a new s-note from SAP or incorrect values in the technical table. Every SAP table can be changed via SE16 or SE11 transaction - all you need to have is a <mark> debug with change role</mark> assigned to your user. In this article you can find youtube video, and bellow is detailed step by step instruction.

<h2>Video tutorial</h2>
<div style="text-align:center;">
<iframe width="560" height="315" src="https://www.youtube.com/embed/evxRzGTY5lE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

<h2>Step by step instruction how to change entry in SE16</h2>
1. We have to login into the system and go to the SE16 or SE11 transaction. Put the table name, and display the required result. When you see the record which you want to edit, please select it and put  **/hs** in the transaction textbox.

{{<figure align=center src="/se16_se11_change/1.png" width="80%" alt="se11 window" >}}

2. Click on the Display icon in the upper panel. Normally you should see a detailed view, but now the debugger will run instead. This step will not work if you do not have the debug authorization.

{{<figure align=center src="/se16_se11_change/1a.png"  width="80%" alt="se11 table" >}}

3. In the debugger window, please click on **Breakpoints-> Breakpoint at-> Breakpoint at Subroutine**. New window should open.
{{<figure align=center src="/se16_se11_change/2.png"  width="80%" alt="Breakpoint window" >}}

4. Click on the FORM tab, and put **SAPLSETB** in the program and **SET_STATUS_VAL** in Fmla. No please press F8 - program should stop on refresh_exclude_tab.

{{<figure align=center src="/se16_se11_change/3.png"  width="80%" alt="Create Breakpoint window" >}}

5. Please double click on the code variable, it should appear in the right bottom corner. Now you have to click on the edit icon and change the variable value from SHOW to EDIT. Please press F8 to continue executing. 

{{<figure align=center src="/se16_se11_change/4.png"  width="80%" alt="Variable change" >}}

6. You should be able to change the values of your entry without any restriction. Please be informed that in the EDIT case you can't add entires. To insert new line into the table, please use ANVO.

{{<figure align=center src="/se16_se11_change/5.png"  width="80%" alt="Edit mode" >}}

Before you save the entry, please double check the consequences. Editing the tables directly on production is not the best idea.