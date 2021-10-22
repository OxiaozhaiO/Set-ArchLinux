下載軟體：
https://github.com/Fndroid/clash_for_windows_pkg/releases/tag/0.17.1

解壓後運行./cfw

在主界面的General選項卡中打開“Allow LAN”
然後在Profile選項卡界面中的上方輸入欄中複製訂閱鏈接，點擊Download即可

然後更改配置文件：
sudo chmod 666 /etc/environment
vi /etc/environment
輸入以下代碼：
http_proxy=http://127.0.0.1:7890/
https_proxy=http://127.0.0.1:7890/
ftp_proxy=http://127.0.0.1:7890/
HTTP_PROXY=http://127.0.0.1:7890/
HTTPS_PROXY=http://127.0.0.1:7890/
FTP_PROXY=http://127.0.0.1:7890/

再把文件改回只讀
sudo chmod 444 /etc/environment
然後重啓電腦
/*如果不添加有效的節點修然後修改配置文件，重啓會導致斷網*/
