# nginx-configure

nginx configuration tweaked to make the best of every modern browser capability
- http/2
- ~~brotli~~*
- TLS 1.3, 1.2
- *cache all the things!*
- header security defaults that make the dev console stop bleeding security warnings 

## notes
- brotli will have to be compiled against the version of nginx being used, to create the module plugin, which can be symlinked to e.g. `/etc/nginx/modules`, and enabled in the nginx config
