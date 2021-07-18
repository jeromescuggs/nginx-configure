# nginx-configure

nginx configuration tweaked to make the best of every modern browser capability
- http/2
- brotli* to really supercharge your compression, hand in hand with gzip
- TLS 1.3, 1.2
- *cache all the things!*
- header security defaults that make the dev console stop bleeding security warnings 

## notes
- brotli will have to be compiled against the version of nginx being used, to create the module plugin, which can be symlinked to e.g. `/etc/nginx/modules`, and enabled in the nginx config

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
make modules
cp objs/*.so /usr/lib/nginx/modules/
nginx -t
systemctl restart nginx 
```
