---
title: "How to contribute ABAP projects on Github"
date: 2021-12-01T22:01:24+02:00
tags: ["ABAP","Github","ABAPGit"]
lastmod: 2021-12-07T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Last time, when I published my bw_toolbox project on Github, there was a lot of questions from regular developers not so much familiar with git, how they can contribute. Because of that, I decided to write this quick-start tutorial.

What do I need? – system requirements
Connection with GitHub – your instance should be able to establish a connection with github.com,
SSL Entires – you have to configure your SAP System by adding necessary certificates into STRUST transaction (details),
Profile configuration – also changes on the profile level are required, so you have to manual edit entries or use transaction (details).
ABAP implementation of git – ABAPGit – this program can be downloaded by copy-paste from it’s GitHub page.
As you see this is a quite specific configuration, and usually this can’t be done on our client instances. Because of that, a good idea is to install your own SAP Instance. For details please check article bellow or my youtube video.

Official SAP Blog post: https://blogs.sap.com/2018/10/16/sap-as-abap-7.5x-developer-editions-faqs/

My youtube tutorial: https://youtu.be/Mk9dslG-_RU

Step by step
1. Install your ABAPGit instance, by copy/paste a zabapgit report form the repository: https://github.com/abapGit/abapGit. More information here.
<img src="/how_to_contribute/contribution1.gif" width="80%" />

2. Set up your certificates and profiles as described in the official wiki

3. Create and log in to your GitHub account. Next find & fork project which you want to contribute by click „Fork” button.
<img src="/how_to_contribute/contribution2.gif" width="80%" />

4. Now forked project should be added to ABAPGit
<img src="/how_to_contribute/contribution3.gif" width="80%" />

5. Now it is time do do your changes
<img src="/how_to_contribute/contribution4.gif" width="80%" />

6. Let’s now push changes to our repository
<img src="/how_to_contribute/contribution5.gif" width="80%" />

7. Now as you can see on your github page, code has been updated
<img src="/how_to_contribute/contribution6.png" width="80%" />

8. So we have to create a pull request to the original repository
<img src="/how_to_contribute/contribution7.gif" width="80%" />

9. Now please wait until author will accept the changes
<img src="/how_to_contribute/contribution8.png" width="80%" />


That is all 🙂

Have a good time during your contributions !