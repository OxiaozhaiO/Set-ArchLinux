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
### GPT格式
摁下「g」創建GPT格式表
```java 
1. 摁下「n」創建一個分區(作為引導)
2. 提示「輸入磁碟編號」,摁ENTER選擇默認(這個分區位置為「/dev/sda1」)
3. 然後提示「從哪裡(2048~xxxx)」,摁ENTER選擇最開頭
4. 然後提示「到哪裡」,通常都是「+512M」
5. 然後ENTER,如果有讓你輸入yes/no的就輸入yes
6. 引導分區建好了
7. 之後就是swap
8. 還是同樣的做法摁「n」建立,但編號選擇「3」,提示「到哪裡」時,根據自己的情況加,我就輸入我的記憶體大小「+8G」
9. 然後主分區狂摁ENTER就好了
10.最後摁「w」寫入
```
### 設置分區格式
```java
/dev/sda1:引導(fat32)
/dev/sda2:主分區(ext4)
/dev/sda3:swap(swap)
```
```java
mkfs.fat -F32 /dev/sda1
mkfs.ext4 /dev/sda2
mkswap /dev/sda3
swapon /dev/sda3
```
## 2.掛載
掛載的原因：我們是在隨身碟裏的系統工作,訪問不了磁碟,安裝也是安裝在隨身碟裏,所以要把磁碟掛載到隨身碟裏的系統裏
```java
mount /dev/sda2 /mnt  //將主分區掛載到/mnt目錄
```
創建/boot路徑,將/dev/sda1(引導)掛載到/boot
```java
mkdir /mnt/boot
mount /dev/sda1 /mnt/boot
```
##  3.安裝
```java
pacstrap /mnt base linux linux-firmware  /安裝到掛(磁)載(碟)的目錄裡面
genfstab -U /mnt >> /mnt/etc/fstab  //生成fstab
```
### 一系列設置
```java
vim /mnt/etc/locale.gen  //用vim打開locale.gen
```
將這三個取消註釋    
![](https://github.com/XxiaozhaiX/images/blob/main/fdisk/locale.gen.png)  
  
進入系統    
```java
arch-chroot /mnt  //進入安裝好的系統
ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime  //設置本地時間
hwclock --systohc  //同步時間
locale-gen  //更新locale-gen
passwd  //設置密碼
exit  //退出系統
```
設置locale.conf   
```java
vim /mnt/etc/locale.conf
輸入「LANG=en_US.UTF-8」
```
設置機器名
```java
vim /mnt/etc/hostname
```
編輯hosts
```java
vim /mnt/etc/hosts
輸入:
127.0.0.1     localhost
::1           localhost
127.0.0.1     <機器名>.localdomain  <機器名>
```
## 4.萬惡之源———grub引導
進入安裝好的系統  
```java
arch-chroot /mnt
```
安裝grub及相關軟體 
```java
pacman -S grub efibootmgr intel-ucode os-prober  //intel的CPU安裝intel-ucode   amd的CPU安裝amd-ucode
```
創建/grub資料夾並生成grub文件 
```java
mkdir /boot/grub
grub-mkconfig > /boot/grub/grub.cfg
grub-mkconfig -o /boot/grub/grub.cfg  //新版
```
查看電腦架構  
```java
uname -m  //我這邊是x86_64
```
grub安裝架構版本
```java
grub-install --target=x86_64-efi --efi-directory=/boot  //x86_64
grub-install --target=i386-pc /dev/sda  // MBR and BIOS
```
## 5.安裝軟體
我安裝我所需要的軟體
```java
pacman -S vim  //最好用的編輯器
pacman -S zsh  //如果bash是cmd,那麼zsh就是powershell
pacman -S dhcpcd  //動態分配地址軟體
pacman -S wpa_supplicant  //連網工具
```
## 6.安裝完成後
重新啟動
```java
reboot
```
拔下隨身碟
## 7.事後
### 安裝失敗怎麼办
#### 1.先安裝Manjaro,然後將其覆蓋
#### 2.把磁碟吃了
安裝中文和英文字體：
```java
sudo pacman -S ttf-dejavu wqy-microhei
```
dhcpcd開機啟動
```java
sudo systemctl enable dhcpcd
```
添加sddm(如果安裝了桌面環境)
```java
sudo systemctl enable sddm
```
