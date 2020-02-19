# Install new liferay instance

Clone this repo to a temp folder. \
`git clone xxx .`

## Install required packages
`apt get update` \
`sudo apt-get install libncurses5` \
`sudo apt-get install nginx`

Copy example nginx site to `/etc/nginx/site-available` \ 
_the .ssl version is a guideline for after installing certbot, we adjust the automated config adjust by certbot a bit (snippets/)_  

Edit example file to your needs \
Symlink config file in enabled sites. \
`sudo ln -s /etc/nginx/sites-available/<site> /etc/nginx/sites-enabled/<site>` \
Test nginx config
`sudo nginx -t` \
Reload nginx config
`sudo nginx -s reload` \

## Install certbot
`wget https://dl.eff.org/certbot-auto`

`sudo mv certbot-auto /usr/local/bin/certbot-auto`

`sudo chown root /usr/local/bin/certbot-auto`

`sudo chmod 0755 /usr/local/bin/certbot-auto`

`sudo /usr/local/bin/certbot-auto --nginx`

Auto renewal should be present in /etc/cron.d/<certbot> if not you can copy the snippet

### adjust nginx config with ssl part (snippet)
`sudo cp -r snippets /etc/nginx/` 
edit your site config

## Install liferay
`wget https://bitnami.com/redirect/to/712122/bitnami-liferay-7.2.0-4-linux-x64-installer.run` 

Give exec rights to bitname installer \
`chmod +x bitnami-liferay-7.2.0-4-linux-x64-installer.run`

`sudo ./bitnami-liferay-7.2.0-4-linux-x64-installer.run`

### adjust tomcat server.xml
- append tomcat-server-snippet.xml contents to `/opt/liferay-7.2.0-4/apache-tomcat/conf/server.xml`

## Autostart of tomcat (after server reboot)
`sudo cp tomcat /etc/init.d/`
`sudo chmod +x /etc/init.d/tomcat`
`sudo systemctl enable tomcat`

# Reboot system to check all succeeded
