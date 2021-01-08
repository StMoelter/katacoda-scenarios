FROM nginx:1.19.6-alpine
COPY default.conf /etc/nginx/conf.d/default.conf
COPY .htpasswd /etc/nginx/.htpasswd
COPY index.html /usr/share/nginx/html/index.html
RUN mkdir /usr/share/nginx/html/protected
COPY secret.html /usr/share/nginx/html/protected/index.html


# CMD ["nginx", "-g", "daemon off;"]

