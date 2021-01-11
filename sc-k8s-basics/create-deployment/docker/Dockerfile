FROM nginx:1.19.6-alpine
RUN mkdir /usr/share/nginx/html/protected
RUN mkdir /etc/nginx/auth/
COPY default.conf /etc/nginx/conf.d/default.conf
COPY .htpasswd /etc/nginx/auth/.htpasswd
COPY index.html /usr/share/nginx/html/index.html
COPY secret.html /usr/share/nginx/html/protected/index.html


# CMD ["nginx", "-g", "daemon off;"]

