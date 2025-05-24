# Basics

## File movement

Force move a file

> `sudo mv -f -i <source> <destination>`

## Directory management

Remove full directory

> `rm -r <directory>`

## Screen commands

List screens

> `screen -ls`

Reattach to screen

> `screen -r <screenName>`

Detach from screen

> `screen -d` or ctrl + a + d

Kill a screen

> `screen -X -S [screen to kill] kill`

## Symlinking

Copy and remove symlink files/folder

> `sudo cp -r folder /destination`  
> `sudo find . -type f -exec chmod -x {} +` 
> `sudo find . -type d -exec chmod 755 {}`  

Symlink folder to git

> `mkdir -p ~/path_to_git/dotfiles/name_of_pkg/.config/name_of_pkg`  
> `cp -r ~/path_to_pkg/ ~/path_to_git/dotfiles/pkg_name/.config`    
> `rm -r ~/path_to_pkg/*`   
> `stow -t ~ pkg_name`  


## WiFi management

show current connections

> `nmcli connection show`

show wifi device status

> `nmcli device status`

show all available devices

> `nmcli -f SSID device wifi list`

connect to device

> `nmcli device wifi connect "WIFI_NAME"`

delete connection

> `nmcli connection delete "WIFI_NAME"`

disconnect from device

> `nmcli device disconnect wlan0`


## Hyprlinux

pacman is currently in use

> `sudo rm /var/lib/pacman/db.lck`

create new fish bind    
vim a file with shortcut_name.fish

> `function funcName      
>       cmd to execute   
>     end` 

> `funcsave funcName`
