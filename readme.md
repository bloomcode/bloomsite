# Bloomcode home page

Currently served by Node/Express from a DigitalOcean Ubuntu droplet.

## PM2

[PM2](https://www.npmjs.com/package/pm2) is installed globally on the server, and should restart our app automatically if anything crashes.

## Colors

These were taken from our company mascot, the beautiful [Forget-me-not](http://en.wikipedia.org/wiki/Forget-me-not)

```
gray: #655d5b
purple: #692776
blue: #007fe6
```

## Initial setup

Unix demands the blood of your first-born. To appease, use the following incantations

```
ssh root@198.199.108.34
adduser bcadmin
gpasswd -a bcadmin sudo

ssh bcadmin@198.199.108.34
sudo apt-get --purge remove node
sudo apt-get --purge remove nodejs
sudo apt-get --purge remove nodejs-legacy
sudo apt-get install curl
sudo apt-get install git
sudo apt-get install npm
sudo npm cache clean -f
sudo npm install -g n
sudo n latest
sudo npm install pm2 -g
sudo setcap cap_net_bind_service=+ep /usr/local/bin/node

cd /home/bcadmin/bloomsite
sudo npm install

pm2 start bloomsite.js
pm2 save
sudo env PATH=$PATH:/usr/local/bin pm2 startup systemd -u bcadmin
```
