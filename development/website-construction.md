# Local setup

## SSH

Copy the rsa pub contents after creation and place in .ssh/authorized_keys 
Typcial path: ~/.ssh/id_rsa

> `ssh-keygen -t rsa -b 4096 -C "emailAddress@gmail.com"`

Create the config file in the .ssh directory

> `Host my-website`
>   `HostName \[VM_EXTERNAL_IP]`
>   `User \[ACCOUNT_USERNAME]`
>   `IdentityFile ~/.ssh/id_rsa`


## HTTPS setup

Install certbot

> `sudo apt update`
> `sudo apt install certbot`

Install ssl certificate

> `sudo certbot --nginx (or apache)`

Check /etc/nginx/sites-available/ for the website name in default file  
If not present add and reload nginx

> `server {
>   listen 80;
>   server_name example.com www.example.com;`

Renew expired certificate

> `sudo certbot --force-renewal`
> `sudo nginx reload`
> copy keys from /etc/letsencrypt/live/websitename/  to backend key folder 
