server {
        listen 443 ssl http2;
        listen       [::]:443;
        server_name  www.portfolio-alberto.es portfolio-alberto.es;
        root         /var/www/html/portfolio;
        include /etc/nginx/ssl/*.conf;
        location / {
        }
        error_page 404 /error404/index.html;
        location = /error404/index.html {
        }
        error_page 500 502 503 504 /50x.html;
        #location = /50x.html {
        #}
	add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload ";
    }

server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name _;
        return 301 https://$host$request_uri;
}

server {
        listen       443 ssl http2;
        listen       [::]:443;
        server_name  www.win.portfolio-alberto.es win.portfolio-alberto.es;
        include /etc/nginx/ssl/*.conf;
        #index index.php  index.html index.htm;
        error_page 404 /error404/index.html;
        location = /error404/index.html {
        }
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
        location / {
                proxy_pass http://3.140.93.65:80;
        }
	add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload ";       }

server {
        listen       443 ssl http2;
        listen       [::]:443;
        server_name  www.tienda.portfolio-alberto.es tienda.portfolio-alberto.es;
        include /etc/nginx/ssl/*.conf;
        #index index.php  index.html index.htm;
        error_page 404 /error404/index.html;
        location = /error404/index.html {
        }
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
	location / {
		proxy_pass http://127.0.0.1:8080;
	}
    }

server {
        listen       443 ssl http2;
        listen       [::]:443;
        server_name  www.node.portfolio-alberto.es node.portfolio-alberto.es;
        #return 301 https://tienda.portfolio-alberto.es$request_uri;
        #root         /var/www/html/wordpress;
        include /etc/nginx/ssl/*.conf;
        #index index.php  index.html index.htm;
        error_page 404 /error404/index.html;
        location = /error404/index.html {
        }
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
        location / {
               proxy_pass http://127.0.0.1:5000;
        }
    }
