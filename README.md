# ModernWMS - Warehouse Management System

<div align="center">
  <img src="logo.png" alt="ModernWMS logo" width="200" height="auto" />
  <h1>ModernWMS</h1>
  <p>A simple, complete and open source warehouse management system</p>

<!-- Badges -->
[![License: MIT](https://img.shields.io/badge/license-MIT-orange.svg)](https://opensource.org/licenses/MIT/)
![Release Version (latest Version)](https://img.shields.io/github/v/release/fjykTec/ModernWMS?color=orange&include_prereleases)
![QR Code Support](https://img.shields.io/badge/QR--Code-Support-orange.svg)
![Docker Support](https://img.shields.io/badge/Docker-Support-orange.svg)
![i18n Support](https://img.shields.io/badge/i18n-Support-orange.svg)
[![MySQL8](https://img.shields.io/badge/MySQL8.0-Support-orange)](https://www.mysql.com/downloads/)
[![SQL Server](https://img.shields.io/badge/SQL%20Server2017%2B-Support-orange)](https://www.mysql.com/downloads/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL12-Support-orange)](https://www.mysql.com/downloads/)

![repo size](https://img.shields.io/github/repo-size/fjykTec/ModernWMS)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/fjykTec/ModernWMS)
<!--![Contributors](https://img.shields.io/github/contributors/fjykTec/ModernWMS?color=blue) -->

![GitHub Org's stars](https://img.shields.io/github/stars/fjykTec/ModernWMS?style=social)
![GitHub Follows](https://img.shields.io/github/followers/ModernWMS?style=social)
![GitHub Forks](https://img.shields.io/github/forks/fjykTec/ModernWMS?style=social)
![GitHub Watch](https://img.shields.io/github/watchers/fjykTec/ModernWMS?style=social)
![Gitee Stars](https://gitee.com/modernwms/ModernWMS/badge/star.svg?theme=social)
![Gitee Forks](https://gitee.com/modernwms/ModernWMS/badge/fork.svg?theme=social)

![.NET](https://img.shields.io/badge/.NET-7.0.0-green)
![Vuetify Cli](https://img.shields.io/badge/Vuetify/cli-3.0.4-green)
![Vue](https://img.shields.io/badge/Vue-3.2.45-green)
![TypeScript](https://img.shields.io/badge/TypeScript-4.1.2-green)
![VXE Table](https://img.shields.io/badge/VXETable-4.3.7-green)
![Vite](https://img.shields.io/badge/Vite-4.0.0-green)
![NodeJS](https://img.shields.io/badge/NodeJS-16.13.1-green)
</div>
<div align="center">
  <h3>
  <a href="../../blob/master/README.zh-CN.md">中文文档</a>
  </h3>
  <h3>
  <a href="https://modernwms.ikeyly.com">Home Page</a>
  </h3>
</div>

# Contents

- [ModernWMS - Warehouse Management System](#modernwms---warehouse-management-system)
- [Contents](#contents)
  - [Introduction](#introduction)
  - [Requirements](#requirements)
    - [Linux OS](#linux-os)
    - [Windows OS](#windows-os)
  - [Installation](#installation)
    - [Linux](#linux)
    - [Windows](#windows)
    - [Docke(Optional)](#dockeoptional)
  - [Usage](#usage)
  - [Contact](#contact)
  - [License](#license)

## Introduction 

  The inventory management system is a set of small logistics warehousing supply chain processes that we have summarized from years of ERP system research and development. In the process of work, many of our small and medium-sized enterprises, due to limited IT budget, cannot use the right system for them, but there are real needs in warehouse management, that's how we started the project. To help some people who need it.

## Requirements

### Linux OS

+ Ubuntu 18.04(LTS),20.04(LTS),22.04(LTS)
+ CentOS Stream 8,9
+ RHEL 8(8.7),9(9.1)
+ Debian 10,11
+ openSUSE 15

### Windows OS

+ Windows 10(1607+),11(21H2+)
+ Windows Server 2012+

## Installation

### Linux

+ download the source code and compile
  + Step 1, download the source code

  ```bash
  cd /tmp/ && wget https://github.com/fjykTec/ModernWMS/archive/refs/heads/master.zip
  ```  

  + Step 2, Install .NET SDK, Runtime and NodeJS

  ```bash
  wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
  sudo dpkg -i packages-microsoft-prod.deb
  sudo apt-get update && sudo apt-get install -y dotnet-sdk-7.0
  sudo apt-get install -y aspnetcore-runtime-7.0
  curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
  sudo apt install -y nodejs
  ```  

  + Step 3, compile frontend and backend

  ```bash
  cd /tmp/ && unzip master.zip && cd ./ModernWMS-master
  mkdir -p /ModernWMS/frontend/ /ModernWMS/backend/
  cd ./frontend/ && yarn && yarn build && cp -rf ./frontend/dist/* /ModernWMS/frontend/
  cd ./backend/ && sudo dotnet publish && cp -rf ./backend/ModernWMS/bin/Debug/net7.0/publish/* /ModernWMS/backend/
  ```  

  + Step 4, Install Nginx

  ```bash
  cd /tmp/ && wget http://nginx.org/download/nginx-1.18.0.tar.gz 
  tar -zxvf nginx-1.18.0.tar.gz && cd nginx-1.18.0
  ./configure --prefix=/etc/nginx --with-http_secure_link_module --with-http_stub_status_module --with-http_ssl_module --with-http_realip_module
  make && make install
  cp -rf /ModernWMS/frontend/* /etc/nginx/html/
  dotnet /ModernWMS/backend/ModernWMS.dll --urls http://0.0.0.0:20011
  ```  
  
### Windows

+ download the source code and compile
  + Step 1, download the source code
  ```PowerShell
  cd c:\
  wget -Uri https://github.com/fjykTec/ModernWMS/archive/refs/heads/master.zip  -OutFile master.zip
  Expand-Archive -Path C:\master.zip -DestinationPath C:\
  ```
  + Step 2, Install .NET SDK, .NET Runtime and NodeJS
  ```CMD
  wget -Uri https://download.visualstudio.microsoft.com/download/pr/35660869-0942-4c5d-8692-6e0d4040137a/4921a36b578d8358dac4c27598519832/dotnet-sdk-7.0.101-win-x64.exe  -OutFile dotnet-sdk-7.0.101-win-x64.exe
  dotnet-sdk-7.0.100-win-x64.exe /install /quiet /norestart
  wget -Uri https://nodejs.org/dist/v16.13.1/node-v16.13.1-x64.msi  -OutFile node-v16.13.1-x64.msi
  msiexec /i .\node-v16.13.1-x64.msi /passive /norestart
  ```
  + Step 3, compile frontend and backend
  ```
  md C:\ModernWMS\frontend\
  md C:\ModernWMS\backend\
  cd c:\ModernWMS-master\backend
  dotnet publish 
  copy-item -path ".\backend\ModernWMS\bin\Debug\net7.0\publish\" -destination "C:\ModernWMS\backend\" -recurse
  copy-Item ".\backend\ModernWMS\wms.db" -Destination "C:\ModernWMS\backend\"
  cd c:\ModernWMS-master\frontend  
  yarn && yarn build 
  copy-item -path ".\frontend\dist\*" -destination "C:\ModernWMS\frontend\" -recurse
  ```
  + Step 4, Install Nginx
  ```
  cd C:\
  wget -Uri http://nginx.org/download/nginx-1.16.1.zip -OutFile nginx-1.16.1.zip
  Expand-Archive -Path C:\nginx-1.16.1.zip -DestinationPath C:\
  copy-item -path "C:\ModernWMS\frontend\*" -destination ".\nginx-1.16.1\html\" -recurse
  start .\nginx-1.16.1\nginx.exe
  cd C:\ModernWMS\backend\
  dotnet ModernWMS.dll --urls http://0.0.0.0:20011
  ```

### Docke(Optional)

+ download the source code and compile
  + Step 1, download the source code

  ```bash
  cd /tmp/ && wget https://github.com/fjykTec/ModernWMS/archive/refs/heads/master.zip
  ```  
  
  + Step 2, compile frontend and backend
  
  ```bash
  cd /tmp/ && unzip master.zip && cd ./ModernWMS-master
  cd ./frontend/ && yarn && yarn build && cp -rf ./frontend/dist/* ./docker/frontend/
  cd ./backend/ && sudo dotnet publish && cp -rf ./backend/ModernWMS/bin/Debug/net7.0/publish/* ./docker/backend/
  cp -rf ./backend/ModernWMS/wms.db ./docker/backend/
  ```  
  + Step 3, deploy
  ```shell
  cd /tmp/ModernWMS-master/docker/
  docker build -t modernwms:1.0 .
  docker run -d -p 80:80  modernwms:1.0 /bin/bash ./run.sh
  ```

## Usage

  ```shell
  Accessing ip address (http://127.0.0.1 or http://the IP address you depolyed) via web browser 
  
  Account: admin 
  Password: 1
  ```

  <h4>
    <a href="https://wmsonline.ikeyly.com">Demo</a>
  </h4> 

  <img src="image2.png" alt="image2" height="auto" />

  <img src="image0.png" alt="image0" height="auto" />

  <img src="image1.png" alt="image1" height="auto" />
  
## Contact

<h4>
  <a href="https://github.com/fjykTec/ModernWMS/issues/new?template=bug_report.md&title=[BUG]">Report a BUG</a>
</h4>
<h4>
  <a href="https://github.com/fjykTec/ModernWMS/issues/new?template=feature_request.md&title=[FR]">Submit a suggestion</a>
</h4>
<h4>
  <a href="https://jq.qq.com/?_wv=1027&k=YgVJGWnI">Join QQ Group Chat 757128595</a>
</h4>

## License

Distributed under the [MIT](https://opensource.org/licenses/MIT/) License. See [LICENSE.txt](https://github.com/fjykTec/ModernWMS/master/LICENSE) for more information.This must be observed.
