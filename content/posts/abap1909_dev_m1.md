---
title: "How to install ABAP 1909 on mac M1"
date: 2021-11-10T20:44:24+02:00
tags: ["ABAP","Installation","docker","M1","Apple Silicon","ABAP_trial","A4H"]
editPost:
    URL: "https://github.com/pawelwiejkut/pawelwiejkut.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

How to run ABAP 1909 on MacOs with M1 ? For me the best idea was to use UTM. I also tried before with docker without success - at the end there was always an error.

1. Install [UTM](https://mac.getutm.app)
2. Download [Ubuntu Server](https://ubuntu.com/download/server) x64 bit version
3. Create virtual machine on UTM (220 GB storage, 6-7 CPU's, additional flags)
<img src="/utm1a.png" width="80%" />
<img src="/utm2a.png" width="80%" />
<img src="/utm3a.png" width="80%" />
<img src="/utm4a.png" width="80%" />
4. Install Ubuntu server on UTM
5. Install [docker](https://docs.docker.com/engine/install/ubuntu/)
{{< highlight bash >}}
sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

  sudo apt-get update

  sudo apt-get install docker-ce docker-ce-cli containerd.io
{{< /highlight >}}

6. Install [ABAP 1909](https://hub.docker.com/_/sap-abap-trial). Good article also [here](https://blogs.sap.com/2021/02/16/sap-abap-platform-1909-developer-edition-day-1-experience-and-tips-and-tricks/)
{{< highlight bash >}}
docker run --stop-timeout 3600 -i --name a4h -h vhcala4hci -p 3200:3200 -p 3300:3300 -p 8443:8443 -p 30213:30213 -p 30215:30215 -p 50000:50000 -p 50001:50001 -p 50013:50013 -p 50014:50014 store/saplabs/abaptrial:1909 -skip-limits-check -agree-to-sap-license
{{< /highlight >}}

At the beginning it is always running slow. The best idea is to use sgen and regenerate all transactions, then it should be definitely better and pretty usable :)