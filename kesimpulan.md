#  Configuration Nginx ( Localhost ) 

imi adalah contoh konfigurasi docker dengan menggunakan enginx untuk membuat server sendiri tanpa menggunakan xampp,laragon.dan dll jadi hanya menggunakan Doker dengan membuat sebuah kontainer 

## Bangun Docker Image:


```bash
docker build -t my-nginx .
```
## Jalankan Container dengan Volume Mounting:
Jalankan container dengan meng-mount direktori html lokal Anda ke dalam container. Ini akan memastikan bahwa setiap perubahan di direktori html lokal akan langsung tercermin di server Nginx.
```bash
docker run -d -p 8080:80 --name my-nginx-container -v $(pwd)/html:/usr/share/nginx/html my-nginx

docker run -d -p 8080:80 --name my-nginx-container my-nginx

```
## Jika Anda perlu menghentikan dan menghapus container:

```bash
docker stop my-nginx-container
docker rm my-nginx-container
```
## membuat folder 
```bash
mkdir nginx-docker
cd nginx-docker

```
## code enginx
```nginx
events {
    # Blok 'events' digunakan untuk mengatur konfigurasi yang berkaitan dengan penanganan koneksi.
    # Blok ini kosong, berarti menggunakan pengaturan default.
}

http {
    # Blok 'http' berisi konfigurasi untuk server HTTP.
    server {
        listen 80;
        # 'listen 80;' mengatur server untuk mendengarkan pada port 80, port standar untuk HTTP.

        server_name localhost;
        # 'server_name localhost;' menentukan nama server. 'localhost' digunakan sebagai nama server.

        location / {
            root /usr/share/nginx/html;
            # 'root /usr/share/nginx/html;' mengatur direktori root untuk permintaan ke URL yang sesuai dengan blok 'location'.
            # File akan diambil dari direktori '/usr/share/nginx/html'.

            index index.html;
            # 'index index.html;' menentukan file index default yang akan digunakan jika tidak ada file tertentu yang diminta.
            # Dalam hal ini, 'index.html' akan digunakan sebagai file index.
        }

        # Tambahan konfigurasi untuk mendukung akses ke CSS dan JS
        location /css {
            root /usr/share/nginx/html;
            # 'root /usr/share/nginx/html;' mengatur direktori root untuk permintaan ke URL '/css'.
            # File CSS akan diambil dari direktori '/usr/share/nginx/html'.
        }

        location /js {
            root /usr/share/nginx/html;
            # 'root /usr/share/nginx/html;' mengatur direktori root untuk permintaan ke URL '/js'.
            # File JavaScript akan diambil dari direktori '/usr/share/nginx/html'.
        }
    }
}
```
## code ockerfile
```Dockerfile
# Gunakan image Nginx resmi dari Docker Hub
FROM nginx:latest

# Salin file konfigurasi Nginx ke dalam container
COPY ./nginx.conf /etc/nginx/nginx.conf

# Salin seluruh directory html ke dalam direktori Nginx
COPY ./html /usr/share/nginx/html

```
## Structure Fils 
```css
nginx-docker/
│
├── Dockerfile
├── nginx.conf
└── html/
    ├── index.html
    ├── css/
    │   └── styles.css
    └── js/
        └── scripts.js

```

