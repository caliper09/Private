server {
         listen 80;
         root /var/www/pufferpanel;

         server_name panel.examplehost.com;

         location ~ ^/\.well-known {
           root /var/www/html;
           allow all;
         }

         location / {
             proxy_pass http://localhost:8080;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Nginx-Proxy true;
             proxy_http_version 1.1;
             proxy_set_header Upgrade $http_upgrade;
             proxy_set_header Connection "Upgrade";
             proxy_set_header Host $host;
             client_max_body_size 100M;
         }
     }