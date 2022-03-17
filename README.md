# Raspberry pi Ubuntu server Cheatsheet

### Measure temperature
```sh
paste <(cat /sys/class/thermal/thermal_zone*/type) <(cat /sys/class/thermal/thermal_zone*/temp) | column -s $'\t' -t | sed 's/\(.\)..$/.\1°C/'
```

### Docker installation ([reference](https://brjapon.medium.com/setting-up-ubuntu-20-04-arm-64-under-raspberry-pi-4-970654d12696))
```sh
# Docker CE
sudo apt-get update && sudo apt-get upgrade

curl -sSL https://get.docker.com | sh

sudo usermod -aG docker ${USER}

sudo systemctl enable docker

sudo reboot

# Docker compose
sudo apt -y install python3-pip

sudo pip3 install docker-compose

sudo reboot
```

### NVM
```sh
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

source ~/.profile
```

### NGINX ngx_http_js_module (dynamic module)
```sh
#! Required nginx installed on system.

sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install -y libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev

# njs version must match nginx version
wget http://nginx.org/download/nginx-1.18.0.tar.gz
tar -zxvf nginx-1.18.0.tar.gz

sudo apt-get install mercurial
hg clone http://hg.nginx.org/njs

cd nginx-1.18.0
sudo ./configure --with-compat --add-dynamic-module=../njs/nginx
sudo make modules
sudo cp objs/ngx_http_js_module.so /usr/share/nginx/modules

# Add "load_module modules/ngx_http_js_module.so" in /etc/nginx/nginx.conf
```


### Update Tag

```text
git tag -a <<version>> -m "<<comment>>"

git push --tags
```




