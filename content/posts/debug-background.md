---
title: "How to debug background/batch job in SAP ?"
date: 2018-02-17T20:44:24+02:00
tags: ["BW","DTP","job","batch","background"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Today I want to show you a simple way to debug a batch job. Sometimes you just want to debug some process witch default runs in batch. Everything looks simple but you should notice that breakpoints sometimes don’t work in these cases. The situation can be even worst when your job runs only a few seconds.

1. First of all if your job works for a short time, you just should keep him working for a while. To do this you just can create an infinitive loop. So just go to your code and in property place paste:

{{< highlight abap>}}

data: lv_wait.
while lv_wait <> 1.
endwhile.

{{< /highlight >}}

2. Now go to transaction sm50, click on „ALL work process” and then select your process.
<mark>Remember that your background process could run on one of many application servers</mark>

<img src="/debug_background/1.png" width="80%" />

3. Click on Administration-> Program -> Debugging.

<img src="/debug_background/2.png" width="80%" />

4. After confirming the pop-up you should see a debugger.

<img src="/debug_background/3.png" width="80%" />

