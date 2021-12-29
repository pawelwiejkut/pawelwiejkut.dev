---
title: "How to check who deleted your BW object?"
date: 2021-01-10T20:44:24+02:00
tags: ["BW","hack","slg0"]
lastmod: 2021-12-10T00:00:00+02:00
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Most of the objects are not modifiable on the quality or production systems, but we have exceptions like Infopackages on BW. Yesterday I have to check who deleted an object from the system and fortunately, there is the log for this operation. I will show you how to check this.

1. We have to go to the transaction SGL1 and search for RSSM
<img src="/check_who_deleted/1.png" width="80%" />

2. Now you should be able to find the impostor 🙂
<img src="/check_who_deleted/2.png" width="80%" />


