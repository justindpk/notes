# Set Up / Repair ArchLinux

## Steps to set up

list drives

> $ fdisk -l

create 3 partitions

> $ fdisk /dev/sda1
> $ fdisk /dev/sda2
> $ fdisk /dev/sda3

format partitions

> $ mkfs.fat -F 32 /dev/sda1
> $ mkswap -F /dev/sda2
> $ mkfs.ext4 /dev/sda3

mount partitions

> $ mount /dev/sda3 /mnt
> $ mount --mkdir /dev/sda1/ /mnt/boot
> $ swapon /dev/sda2

install wifi

> $ ip link
> $ iwctl
> $ device list
> $ station device_name scan
> $ station device_name get-networks
> $ station device_name connect SSID

install linux

> $ pacstrap -K /mnt base linux linux-firmware

set partition to mount on boot

> $ genfstab -U /mnt >> /mnt/etc/fstab

install vim

> $ pacman -S vim
> $ export EDITOR = vim

localization

> $ vim /etc/locale.gen

> $ vim /etc/locale.conf

network config

> $ pacman -S networkmanager

> $ systemctl enable NetworkManager

change password & create user

> $ passwd
> $ pacman -S sudo
> $ useradd -m {username}
> $ passwd {username}
> $ usermod -aG wheel {username}
> $ visudo
> $ passwd {username}

install bootloader

> $ pacman -S grub efibootmgr
> $ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}
> $ grub-mkconfig -o /boot/grub/grub.cfg
> $ exit
> $ reboot

wifi

> $ nmcli device wifi connect {SSID} password {passowrd}

install paru

> $ vim /etc/pacman.conf

> $ sudo pacman -Syu
> $ sudo pacman -S git base-devel
> $ git clone https://aur.archlinux.org/paru.git
> $ cd paru
> $ makepg -si
> $ cd .. && rm -rf paru
> $ paru

install hyprland and kitty

> $ paru -S hyprland-git kitty gtk3

edit hyprland config

> $ sudo vim ~/.config/hyprland/hyprland.conf

## Repair Linux

boot linux from repair usb [ensure usb has archlinux]

</aside>

mount partitions

> $ mount /dev/sda3 /mnt
> $ mount --mkdir /dev/sda1 /mnt/boot
> $ swapon /dev/sda2

reinstall linux

> $ pacstrap /mnt base linux linux-firmware [corrupted package] [--overwrite \*]

generate fstab

> $ genfstab -U /mnt >> /mnt/etc/fstab

chroot

> $ arch-chroot /mnt

repair GRUB

> $ grub-install /dev/sda
> $ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}

exit / unmount

> $ exit
> $ unmount -R /mnt
> $ reboot

</aside>
