
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
syslinux-install_update -iam
nano /boot/syslinux/syslinux.cfg
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

sudo pacman -Suy

sudo pacman -S yaourt

sudo pacman -S pulseaudio pulseaudio-alsa jack2 ffmpeg 
sudo pacman -S xorg
sudo pacman -S xorg-xinit xorg-twm xterm
sudo pacman -S xorg-server xorg-server-utils xorg-server-xwayland xorg-xkill
sudo pacman -S xf86-input-synaptics xf86-input-mouse xf86-input-keyboard xf86-wacom xf86-input-libinput

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
system enable gdm

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



	  
sudo nano ~/.xinitrc
#exec cinnamon-session
#exec enlightenment_start
#exec gnome-session
#exec startkde
#exec startlxqt
#exec mate-session
#exec startxfce4
startx

#-------------------------------------------------------------------------------
#desktop
#-------------------------------------------------------------------------------


sudo pacman -S avahi nss-mdns
systemctl enable avahi-daemon
sudo pacman -S bc rsync mlocate bash-completion pkgstats
sudo pacman -S zip unzip unrar p7zip
sudo pacman -S alsa-utils alsa-plugins lib32-alsa-plugins
sudo pacman -S pavucontrol lib32-libpulse
sudo pacman -S ntfs-3g dosfstools exfat-utils fuse fuse-exfat autofs
sudo pacman -S zramswap
systemctl enable zramswap
sudo pacman -S tlp
systemctl enable tlp
systemctl enable tlp-sleep
systemctl mask systemd-rfkill
tlp start
pause_function
sudo pacman -S terminator synapse shutter galculator compiz conky-lua
sudo pacman -S htop ufw gufw clamav firewalld
systemctl enable firewalld
systemctl enable ufw
sudo pacman -S wine icoutils wine_gecko wine-mono winetricks playonlinux
sudo pacman -S gimp gthumb notepadqq
sudo pacman -S banshee easytag vlc
sudo pacman -S ttf-dejavu ttf-liberation ttf-ms-fonts ttf-vista-fonts


yaourt popcorntime-bin
yaourt teamspeak3
yaourt skype
yaourt google-earth
yaourt dropbox
yaourt moka-icon-theme-git
yaourt nitrux-icon-theme
yauurt numix-icon-theme-git numix-circle-icon-theme-git
yauurt evopop 
yaourt numix-themes
yaourt zuki-themes-git
yaourt google-chrome
yaourt libreoffice

pacman -Rsc
pacman -Qqdt
pacman -Sc

