# Set Up / Repair ArchLinux

---

## Steps to set up

<aside>
💡 list drives

```jsx
$ fdisk -l
```

</aside>

<aside>
💡

create 3 partitions

```jsx
$ fdisk /dev/sda1
$ fdisk /dev/sda2
$ fdisk /dev/sda3
```

</aside>

<aside>
💡 format partitions

```jsx
$ mkfs.fat -F 32 /dev/sda1
$ mkswap -F /dev/sda2
$ mkfs.ext4 /dev/sda3
```

</aside>

<aside>
💡 mount partitions

```jsx
$ mount /dev/sda3 /mnt
$ mount --mkdir /dev/sda1/ /mnt/boot
$ swapon /dev/sda2
```

</aside>

<aside>
💡 install wifi

```jsx
$ ip link
$ iwctl
$ device list
$ station device_name scan
$ station device_name get-networks
$ station device_name connect SSID
```

</aside>

<aside>
💡 install linux

```jsx
$ pacstrap -K /mnt base linux linux-firmware
```

</aside>

<aside>
💡 set partition to mount on boot

```bash
$ genfstab -U /mnt >> /mnt/etc/fstab
```

</aside>

<aside>
💡 install vim

```bash
$ pacman -S vim
$ export EDITOR = vim
```

</aside>

<aside>
💡 localization

```bash
$ vim /etc/locale.gen
```

```bash
$ vim /etc/locale.conf
```

</aside>

<aside>
💡 network config

```bash
$ pacman -S networkmanager
```

```bash
$ systemctl enable NetworkManager
```

</aside>

<aside>
💡 change password & create user

```bash
$ passwd
$ pacman -S sudo
$ useradd -m {username}
$ passwd {username}
$ usermod -aG wheel {username}
$ visudo
$ passwd {username}
```

</aside>

<aside>
💡 install bootloader

```bash
$ pacman -S grub efibootmgr
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}
$ grub-mkconfig -o /boot/grub/grub.cfg
$ exit
$ reboot
```

</aside>

<aside>
💡 wifi

```bash
$ nmcli device wifi connect {SSID} password {passowrd}
```

</aside>

<aside>
💡

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

</aside>

<aside>
💡 install hyprland and kitty

```bash
$ paru -S hyprland-git kitty gtk3
```

</aside>

<aside>
💡 edit hyprland config

```bash
$ sudo vim ~/.config/hyprland/hyprland.conf
```

</aside>

---

## Repair Linux

<aside>
💡 boot linux from repair usb [ensure usb has archlinux]

</aside>

<aside>
💡 mount partitions

```bash
$ mount /dev/sda3 /mnt
$ mount --mkdir /dev/sda1 /mnt/boot
$ swapon /dev/sda2
```

</aside>

<aside>
💡 reinstall linux

```bash
$ pacstrap /mnt base linux linux-firmware [corrupted package] [--overwrite \*]
```

</aside>

<aside>
💡 generate fstab

```bash
$ genfstab -U /mnt >> /mnt/etc/fstab
```

</aside>

<aside>
💡 chroot

```bash
$ arch-chroot /mnt
```

</aside>

<aside>
💡 repair GRUB

```bash
$ grub-install /dev/sda
$ grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id={name it}
```

</aside>

<aside>
💡 exit / unmount

```bash
$ exit
$ unmount -R /mnt
$ reboot
```

</aside>