---
Title: 2023 Spring 第三週
Date: 2023-03-09 11:00
Category: cd2023
Tags: w3, cd2023, wcm2023
Slug: 2023_spring_w3
Author: mdecycu
---

2023 Spring 課程開始第三週, 這個學期起, 開課論述與先前大同小異, 但是執行內容將會有很大的不同.

<!-- PELICAN_END_SUMMARY -->

Stud 與 Stud2 虛擬主機
----

stud.cycu.org 是 2022 Fall 用來建構多人網際內容管理系統的虛擬主機, 由於刪除用戶資料過於繁瑣, 於是選擇重新建立 stud2.cycu.org. 

而建構一台大約兩百多人使用的虛擬主機, 需要下列執行環境:

1. 多人環境下的 Python3 環境, 可以順利執行動態 cmsimde 網際內容管理系統
2. https 的代理伺服器 (stunnel) 與連外的網站數位簽章建置 (letsencrypt)
3. 建立多人帳號所需的準備工作 (使用 newusers 指令)
4. 將所配置的多人帳號資訊, 逐一透過郵件進行通知 (Gmail)
5. 除了先前採 waitress 執行 Flask 網站, 當網站內容變更後 (通常因為 git pull), 需要再利用 hupper -m 執行 server.py, 才能 auto reload

協同產品設計
----

pj1 希望透過 Python remote API 建立一個 browser based 跨網路的機器人足球遊戲, 採 CoppeliaSim 建立. 其中需要在 remoteApiConnections.txt 設定場景主機預定開啟的 ports, 以便讓各 client 能夠經由主機 IPv4 位址 (IPv6 尚無法運作) 中的特定 port 傳送 API 指令. 且各 client 可以由場景主機所啟動的 Visualization Streaming 串流同時觀看運動場景 (內建在 23020 埠號播放).

2023 年 Spring 開始導入 zmqRemoteAPI, 先前的 legacy Python 程式將會隨著新版 CoppeliaSim 的內容架構而逐步退場.

Solid Edge 與 Femap
----

2021 年起 Siemens 開始釋出 Community 版本的 Solid Edge, 允許非營利單位可以免費使用. 同時也提供永久免費的 Femap 讓教育單位使用. 針對這兩項工具的新教育版使用授權, 全球各級學校終於可以更有彈性使用專業的 CAD/E 套件.

Proxy and DNS Servers
----

固定的幾台 Proxy servers 必須定時對系統以及服務更新, 其中包括 3, 4, 42, 53, 69:

sudo apt update

sudo apt upgrade

sudo apt autoremove

sudo /etc/init.d/squid restart

sudo service bind9 restart

for Windows Server connected from Mac RDT need to setup under the admin connect session.

3 and 4 on 209 and 6 (eng) on 0811-2-0-cd02 

Excel 計算平均 =INT(SUM(IF(B2="缺席",0, B2),IF(C2="缺席",0,C2),IF(D2="缺席",0,D2),IF(E2="缺席",0,E2),IF(F2="缺席",0,F2))/5)

Nginx 伺服下的 public_html
----

<pre class="brush:jscript">
sudo_user@cad2:~#sudo vi /etc/nginx/sites-available/default
# 設定讓各用戶的 public_html 目錄可以作為 nginx 伺服網頁目錄
server {
        .....
        .....
        location ~ ^/~(.+?)(/.*)?$ {
              alias /home/$1/public_html$2;
              index  index.html index.htm;
              autoindex on;
        }
# 設定完成後必須重新啟動 nginx
sudo_user@cad2:~# systemctl restart nginx
</pre>

Exam_dot_cycu
----

https 數位簽章更新, 每 90 天必須更新一次

renew certificate (更新數位簽章)

stop nginx service (必須先關閉 nginx 伺服器)

on administrator command window (cmd 在管理者模式下啟動)

execute (執行下列指令)

certbot certonly --standalone

