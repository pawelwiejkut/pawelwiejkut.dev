---
title: "BW Tips and Tricks"
date: 2023-05-29T19:56:19+01:00
tags: ["BW","TIPS","TRICKS"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

### How to add new line character in text variable ?

If you want to add a new line character in text variable of customer exit type, just use standard class:

{{< highlight abap >}}
e_t_range = VALUE #( ( sign = 'I' opt = 'EQ' low = | LINE 1 { cl_abap_char_utilities=>newline } LINE2 | ) ).
{{< /highlight >}}