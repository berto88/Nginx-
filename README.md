//Servidor de mi portfolio:
//tenemos el listen con el puerto por el que escucha
//el server name son las url de entrada
//el root es lo que mostrara, esa es la ruta donde se encuentra mi portfolio
//el include que le indica que ssl(seguridad)recoge 
#SERVER1
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

//Servidor para redireccionar de mi app .net en windows
//tenemos el listen con el puerto por el que escucha
//el server name son las url de entrada
//el root es lo que mostrara, esa es la ruta donde se encuentra mi portfolio
//el include que le indica que ssl(seguridad)recoge 
//el location maneja los errores en las paginas y la redireccion con el proxypass del http al https
//el add_header es para que no se pueda entrar por http

#SERVER2
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
