
loadkeys no-latin1

wifi-menu

ping www.google.com

cfdisk /dev/sda

lsblk /dev/sda #when done to check 

mkfs.ext4 /dev/sdaX #use that on all of them

mkswap /dev/sda2
swapon /dev/sda2

lsblk /dev/sda #when done to check 

mount /dev/sda1 /mnt
mkdir -p /mnt/home
mount /dev/sda3 /mnt/home

lsblk /dev/sda #when done to check 

nano /etc/pacman.d/mirrorlist # dont realy needed

pacstrap -i /mnt base base-devel

genfstab -U -p /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab

arch-chroot /mnt /bin/bash

nano /etc/locale.gen
locale-gen
export LANG=en_US.UTF-8

echo "KEYMAP=no-latin1" >> /etc/vconsole.conf 
cat /etc/vconsole.conf

ln -sf /usr/share/zoneinfo/Europe/Oslo /etc/localtime
hwclock --systohc --utc

echo archpc > /etc/hostname
nano /etc/hosts                # adds to both sides

pacman -S dialog iw wpa_supplicant wpa_actiond
wifi-menu
ip link
systemctl enable netctl-auto@XXXXX.service   # x is usaly wlp something

passwd

pacman -S syslinux gptfdisk efibootmgr dosfstools mtools util-linux
sudo pacman -S memtest86+ wget
syslinux-install_update -iam
cd /boot/syslinux
wget https://projects.archlinux.org/archiso.git/plain/configs/releng/syslinux/splash.png
nano /boot/syslinux/syslinux.cfg

#-----------------------------------------------
 MENU VSHIFT 10

 LABEL memtest
         MENU LABEL Memtest86+
         LINUX ../memtest86+/memtest.bin
		 
#---------------------------------------------------
cp -a /boot /boot.bak
cp -a /boot.bak/* /boot
syslinux-install_update -iam

exit
reboot

#-------------------------------------------------------------------------------
#post-installation
#-------------------------------------------------------------------------------

useradd -m -G wheel -s /bin/bash leif
passwd leif

nano /etc/sudoers   # add it under root

exit
#log in as user

sudo nano /etc/pacman.conf 
# add [archlinuxfr] 
#SigLevel = Never 
#Server = http://repo.archlinux.fr/$arch

# also enable multilab

sudo pacman -Suy

sudo pacman -S yaourt

sudo pacman -S pulseaudio pulseaudio-alsa jack2 ffmpeg 
sudo pacman -S xorg
sudo pacman -S xorg-xinit xorg-twm xterm
sudo pacman -S xorg-server xorg-server-utils xorg-server-xwayland xorg-xkill
sudo pacman -S xdg-user-dirs
xdg-user-dirs-update


#-------------------------------------------------------------------------------
#desktop
#-------------------------------------------------------------------------------

#cinnamon
sudo pacman -S cinnamon

#enlightment
sudo pacman -S enlightenment terminology
sudo pacman -S leafpad epdfview
sudo pacman -S lxappearance

# Gnome
sudo pacman -S gnome gnome-extra telepathy 
sudo pacman -S gedit-plugins gnome-tweak-tool gnome-power-manager gucharmap gvfs-goa
sudo pacman -S deja-dup
yaourt nautilus-share
systemctl enable gdm

# kde
pacmna -S plasma kde-applications kde-l10n-$LOCALE_KDE sddm
systemctl enable sddm

# LXQT
sudo pacman -S lxqt openbox oxygen-icons qtcurve
sudo pacman -S leafpad epdfview
	  
#Mate
sudo pacman -S mate mate-extra
	  
#XFCE
sudo pacman -S xfce4 xfce4-goodies xarchiver mupdf

#i3
sudo pacman -S i3 dmenu

	  
sudo nano ~/.xinitrc
#exec cinnamon-session
#exec enlightenment_start
#exec gnome-session
#exec startkde
#exec startlxqt
#exec mate-session
#exec startxfce4
#exec i3
startx

#-------------------------------------------------------------------------------
#desktop
#-------------------------------------------------------------------------------

sudo pacman -S networkmanager dnsmasq network-manager-applet
sudo pacman -S networkmanager-openconnect networkmanager-openvpn networkmanager-pptp networkmanager-vpnc
sudo pacman -S ntp networkmanager-dispatcher-ntpd
systemctl enable NetworkManager
sudo ntpd -u ntp:ntp
sudo pacman -S bc rsync mlocate bash-completion pkgstats
sudo pacman -S zip unzip unrar p7zip
sudo pacman -S alsa-utils alsa-plugins
sudo pacman -S pavucontrol 
sudo pacman -S ntfs-3g exfat-utils fuse-exfat autofs
sudo pacman -S zramswap
systemctl enable zramswap
sudo pacman -S tlp
systemctl enable tlp
systemctl enable tlp-sleep
systemctl mask systemd-rfkill
tlp start

sudo pacman -S terminator synapse shutter galculator cool-retro-term
sudo pacman -S htop ufw gufw clamav firewalld # firewalld or ufw/gufw
systemctl enable firewalld # just enable one
systemctl enable ufw
sudo pacman -S wine icoutils wine_gecko wine-mono winetricks playonlinux
sudo pacman -S gimp gthumb 
sudo pacman -S banshee easytag vlc
sudo pacman -S ttf-dejavu ttf-liberation 
sudo pacmna -S firefox
sudo pacman -S screenfetch

yaourt ttf-ms-fonts 
yaourt ttf-vista-fonts
yaourt teamspeak3
yaourt skype
yaourt google-earth
yaourt dropbox
yaourt moka-icon-theme-git
yaourt nitrux-icon-theme
yaourt numix-icon-theme-git numix-circle-icon-theme-git
yaourt evopop 
yaourt numix-themes
yaourt zuki-themes-git
yaourt google-chrome
yaourt libreoffice
yaourt compiz
yaourt compiz-manager
yaourt conky-lua
yaourt notepadqq
yaourt steam

pacman -Rsc
pacman -Qqdt
pacman -Sc

# after reboot

systemctl stop netctl-auto@wlp13s0.service
systemctl disable netctl-auto@wlp13s0.service
systemctl disable netctl
#-------------------------------------------------------------------------------
#syslinux
#------------------------------------------------------------------------------



convert -depth 16 -colors 65536 my_custom_image.png splash.png

convert -resize 640×480 -depth 16 -colors 65536 my_custom_image.png splash.png

sudo mv splash.png /boot/syslinux/

UI vesamenu.c32 (I have already uncommented in a previous occasion)
MENU BACKGROUND splash.png

