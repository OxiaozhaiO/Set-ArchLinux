# 安裝ArchLinux
```java
timedatectl set-ntp true  //同步時間
```
## 1.分區
我這邊使用fdisk
```java
fdisk -l //查看磁碟信息
```
![](https://github.com/XxiaozhaiX/images/blob/main/fdisk/main.jpg)
```java
fdisk /dev/sda  //進入磁碟,摁m顯示幫助
```
![](https://github.com/XxiaozhaiX/images/blob/main/fdisk/fdiskdev.png)
根據自己磁碟的格式來選擇  
![](https://github.com/XxiaozhaiX/images/blob/main/fdisk/n.png)
