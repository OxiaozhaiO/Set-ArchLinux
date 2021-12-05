下載軟體：
```java
https://github.com/Fndroid/clash_for_windows_pkg/releases/tag/0.17.1
```
解壓後運行cfw
在主界面的General選項卡中打開“Allow LAN”
![](https://github.com/XxiaozhaiX/images/blob/main/clash/allowlan.png)    

然後在Profile選項卡界面中的上方輸入欄中複製訂閱鏈接，點擊Download即可    
![](https://github.com/XxiaozhaiX/images/blob/main/clash/download.png)

然後更改配置文件：
```java
sudo vim /etc/environment
```
輸入以下代碼：
```java
http_proxy=http://127.0.0.1:7890/
https_proxy=http://127.0.0.1:7890/
ftp_proxy=http://127.0.0.1:7890/
HTTP_PROXY=http://127.0.0.1:7890/
HTTPS_PROXY=http://127.0.0.1:7890/
FTP_PROXY=http://127.0.0.1:7890/
```
然後重啓電腦    
PS:如果不添加有效的節點修然後修改配置文件，重啓會導致斷網
