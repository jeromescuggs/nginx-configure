# nginx-configure

nginx configuration tweaked to make the best of every modern browser capability
- http/2
- brotli* to really supercharge your compression, hand in hand with gzip
- TLS 1.3, 1.2
- *cache all the things!*
- header security defaults that make the dev console stop bleeding security warnings 

## notes

- the defaults assume that you will be generating an SSL certificate using `certbot`. you will need python as well:
```
apt install certbot python3 python3-certbot-nginx
certbot --nginx -d yourwebsite.com -d www.yourwebsite.com
```
- set up certbot for automatic renewals by running `crontab -e` and adding the following: `0 12 * * * /usr/bin/certbot renew --quiet`


- brotli will have to be compiled against the version of nginx being used, to create the module plugin, which can be symlinked to e.g. `/etc/nginx/modules`, and enabled in the nginx config
```
apt install ufw
ufw allow 80
ufw allow 8080
ufw allow 443
ufw allow 22 
ufw enable
```

```
nginx -v
nginx version: nginx/1.21.1
```

```bash
mkdir lab && cd lab
wget http://nginx.org/download/nginx-1.21.1.tar.gz
tar -xvf nginx-1.21.1.tar.gz
git clone https://github.com/google/ngx_brotli
cd nginx-1.21.1
./configure --add-module=../ngx_brotli
make && make install
make modules
cp objs/*.so /usr/lib/nginx/modules/
```
```
cd ..
git clone https://github.com/jeromescuggs/nginx-config
cd nginx-config
```
## \~*open up nginx/nginx.conf, tweak as needed*\~

## \~*edit nginx/sites-avaliable/becausethenet.conf*\~
- copy it to a new file, edit it, do whatever. 

```
cp -r nginx /etc/nginx
```
- to 'enable' the site:
  ```
  cd /etc/nginx
  cp sites-available/yourwebsite.conf sites-enabled/
  ```
```
nginx -t
systemctl enable nginx 
systemctl start nginx
```
