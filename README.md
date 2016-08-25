# Nginx-dynamic-vhost
Simple Nginx vhost which serves multiple projects at once. It uses `project` variable parsed from url to resolve folders for:
1. error logs
2. project public folder

```
server {
        listen 80;
        server_name ~^(?P<project>[a-z0-9]+)\.local$;

        access_log /var/log/nginx/$project.log;
        error_log  /var/log/nginx/$project.log;

        root /home/username/Development/$project/public;
        index   index.php index.html index.htm;

        location / {
                try_files $uri $uri/ /index.php?$args;
        }

        include php.config;
}
```
