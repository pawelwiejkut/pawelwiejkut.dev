---
title: "SAP NPL 7.52 won't start"
date: 2021-04-02T22:01:24+02:00
tags: ["NPL","ABAPTrial","SYBASE","License"]
lastmod: 2021-12-11T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

This time I will show you how to fix the issue with your SAP ABAP Developer instance which don’t want to start. This article is about license issue, which has expired 1.04.2021. In this case command startsap ALL, will stuck on:
{{< highlight bash >}}
Database is not available via R3trans
-------------------------------------------
starting database NPL ...
Log file: /sybase/NPL/startdb.log
{{< /highlight >}}

Or
{{< highlight bash >}}
Stop returns modlib.jslib.caughtException
{{< /highlight >}}

1. We have to download a new license file from https://developers.sap.com/trials-downloads.html?search=ABAP under the section SAP NetWeaver AS ABAP Developer Edition 7.52 SP04
<img src="/npl_wont_start/licsyb1.png" width="80%" />


2. Now we have to login into the system via Terminal on npladm user, type su -l npladm
<img src="/npl_wont_start/licsyb2.gif" width="80%" />


3. We have to backup old license file
{{< highlight bash >}}
sudo cp /sybase/NPL/SYSAM-2_0/licenses/SYBASE_ASE_TestDrive.lic /sybase/NPL/SYSAM-2_0/licenses/SYBASE_ASE_TestDrive.lic.bak
{{< /highlight >}}
<img src="/npl_wont_start/licsyb3.gif" width="80%" />


4. Now lets copy content of SYBASE_ASE_TestDrive.lic from downloaded file and paste this into the file on the system
{{< highlight bash >}}
sudo nano /sybase/NPL/SYSAM-2_0/licenses/SYBASE_ASE_TestDrive.lic
{{< /highlight >}}
<img src="/npl_wont_start/licsyb4.gif" width="80%" />


6. Your server should be able to start your server again without any issues
<img src="/npl_wont_start/licsyb5.gif" width="80%" />

