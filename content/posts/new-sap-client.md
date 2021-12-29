---
title: "Create new SAP client"
date: 2019-06-03T20:44:24+02:00
tags: ["Client","basis"]
aliases : [ new_sap_client ]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

In the SAP NetWeaver system, clients are used for many purposes. One of the business purposes can be handling many sub-companies on one system. From a development perspective, you can use a different client to protect your development or split the system by development and unit tests. Last time I also create a new client on my instance, to separate the client between data to my extractors and rest. How you can achieve this? Let’s start from edit a file on your hard drive.

Operations used for client copy is not complicated. First, of all, you need to add one line at the end of /sapmnt/NPL/profile/DEFAULT.PFL:

{{< highlight bash >}}
nano /sapmnt/NPL/profile/DEFAULT.PFL
login/no_automatic_user_sapstar = 0
{{< / highlight >}}

This will enable to log in on SAP* user, on the new client even if this user does not exist.

<img src="/new_sap_client/1.png" width="80%" />

After the restart we have to add a new logical system name, we can do this in transaction sm30 by edit view: V_TBDLS:

<img src="/new_sap_client/2.png" width="80%" />
<img src="/new_sap_client/3.png" width="80%" />

When a logical client is created, then it is time to go to the scc4 transaction and create a new client:

<img src="/new_sap_client/4.png" width="80%" />

After save, you should be able to log on new client using credentials:

{{< highlight bash >}}
user: SAP* password: pass
{{< / highlight >}}

Unfortunately, the new client is empty and doesn’t have the necessary data, even to create a new user. The simplest way to solve this issue is to copy data from one client to another using transaction **sccl**.

And that’s all! After the copy, you should be able to log in to your new client without issues.





