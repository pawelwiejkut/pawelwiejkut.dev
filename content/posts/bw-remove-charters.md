---
title: "Remove invalid characters in your BW transformation"
date: 2022-01-02T19:56:19+01:00
tags: ["BW","TRFN"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

If you have in your BW regular flat-file data load in your BW system, you probably afflict issues with the wrong data provided by the user. The scenario of this issue can be very simple. It’s enough that the user provides an invalid unsupported charter and during activation, you will get a similar issue:

<img src="/bw_remove_charters/1.png" width="80%" />

# Or other issues like:

Value '#’ (hex. '2300′) of characteristic  contains invalid characters
Error when assigning SID: Action VAL_SID_CONVERT InfoObject
(hex. '500072007A0065006C006500770020006E0061002000720061′) of characteristic  contains inva
This issue also affects me in the last time, and during my research, and found several options for removal. Most of them were based on a simple check like is your charter on the list:

!”%&”()*+,-./:;<=>?_0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ

And this is, of course, true and corresponds to note 173241. But what if you additionally want to check charters provided in the transaction RSKC?

The best way to achieve this is the usage of good FM RSKC_CHAVL_OF_IOBJ_CHECK, which checks charter correctness according to the info object. But by default, this is not a dynamic development. I want to have some dynamic code, which I can paste in every transformation after Datasource and make necessary checks. That’s why I decided to write my own implementation which can handle this issue.

# My implementation
Now all I need to do is add following code like below to the end routine ( consider a move of reference declaration to proper place ):


DATA(lobj_check) = NEW zcl_bw_validate_special(
ir_ref = REF #( result_package ) ).
 
 {{< highlight abap >}}
lobj_check->validate(
  EXPORTING
    it_tab     =  result_package
    it_monitor =  monitor
  IMPORTING
    et_tab     = result_package
    et_monitor =  monitor ).
Now any unsupported charter will be simply replaced by nothing.
{{< / highlight>}}

# Download
You can test this by yourself by getting code from my GitHub page:

https://github.com/pawelwiejkut/bw_remove_charters

Of course please feel free to contribute and create pull requests, or open issues if needed. In the case of AMDP routine, consider usage https://blogs.sap.com/2017/06/15/removing-invalid-and-non-printable-characters-in-hana-based-bw-transformation/.

Thanks for your time and have a great day.


