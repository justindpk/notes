# Set Up / Repair ArchLinux

## Steps to set up

list drives

```jsx
$ fdisk -l
```

create 3 partitions

```jsx
$ fdisk /dev/sda1
$ fdisk /dev/sda2
$ fdisk /dev/sda3
```

format partitions

```jsx
$ mkfs.fat -F 32 /dev/sda1
$ mkswap -F /dev/sda2
$ mkfs.ext4 /dev/sda3
```

mount partitions

```jsx
$ mount /dev/sda3 /mnt
$ mount --mkdir /dev/sda1/ /mnt/boot
$ swapon /dev/sda2
```

install wifi

```jsx
$ ip link
$ iwctl
$ device list
$ station device_name scan
$ station device_name get-networks
$ station device_name connect SSID
```

install linux

```jsx
$ pacstrap -K /mnt base linux linux-firmware
```

set partition to mount on boot

```bash
$ genfstab -U /mnt >> /mnt/etc/fstab
```

install vim

```bash
$ pacman -S vim
$ export EDITOR = vim
```

localization

```bash
$ vim /etc/locale.gen
```

```bash
$ vim /etc/locale.conf
```

network config

```bash
$ pacman -S networkmanager
```

```bash
$ systemctl enable NetworkManager
```

change password & create user

```bash
$ passwd
$ pacman -S sudo
$ useradd -m {username}
$ passwd {username}
$ usermod -aG wheel {username}
$ visudo
$ passwd {username}
```

install bootloader

```bash
$ pacman -S grub efibootmgr
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}
$ grub-mkconfig -o /boot/grub/grub.cfg
$ exit
$ reboot
```

wifi

```bash
$ nmcli device wifi connect {SSID} password {passowrd}
```

install paru

```bash
$ vim /etc/pacman.conf
```

```bash
$ sudo pacman -Syu
$ sudo pacman -S git base-devel
$ git clone https://aur.archlinux.org/paru.git
$ cd paru
$ makepg -si
$ cd .. && rm -rf paru
$ paru
```

install hyprland and kitty

```bash
$ paru -S hyprland-git kitty gtk3
```

edit hyprland config

```bash
$ sudo vim ~/.config/hyprland/hyprland.conf
```

---

## Repair Linux

boot linux from repair usb [ensure usb has archlinux]

mount partitions

```bash
$ mount /dev/sda3 /mnt
$ mount --mkdir /dev/sda1 /mnt/boot
$ swapon /dev/sda2
```

reinstall linux

```bash
$ pacstrap /mnt base linux linux-firmware [corrupted package] [--overwrite \*]
```

generate fstab

```bash
$ genfstab -U /mnt >> /mnt/etc/fstab
```

chroot

```bash
$ arch-chroot /mnt
```

repair GRUB

```bash
$ grub-install /dev/sda
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}
```

exit / unmount

```bash
$ exit
$ unmount -R /mnt
$ reboot
```

</aside>
