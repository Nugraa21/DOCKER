# Gunakan image Nginx resmi dari Docker Hub
FROM nginx:latest

# Salin file konfigurasi Nginx ke dalam container
COPY ./nginx.conf /etc/nginx/nginx.conf

# Salin seluruh directory html ke dalam direktori Nginx
COPY ./html /usr/share/nginx/html
