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


Nginx adalah perangkat lunak server web dan proxy terbalik yang dikenal karena kinerja tinggi, stabilitas, dan kemampuannya untuk menangani banyak koneksi secara efisien. Selain itu, Nginx juga digunakan sebagai load balancer dan caching server.


Nginx (diucapkan "engine x") adalah perangkat lunak server web dan proxy terbalik (reverse proxy) yang digunakan untuk melayani situs web dan aplikasi. Nginx dikenal karena kinerja tinggi, stabilitas, set fitur yang kaya, dan konfigurasi yang sederhana. Berikut adalah beberapa fungsi utama dari Nginx:

1. **Server Web**: Nginx dapat berfungsi sebagai server web yang melayani konten statis (seperti HTML, gambar, dan video) kepada pengguna.

2. **Reverse Proxy**: Nginx dapat bertindak sebagai proxy terbalik, yang berarti dapat meneruskan permintaan dari klien ke server backend (seperti aplikasi web atau database) dan kemudian mengirimkan respons dari server backend kembali ke klien. Ini membantu dalam mengelola lalu lintas dan meningkatkan kinerja serta keamanan.

3. **Load Balancer**: Nginx dapat mendistribusikan beban lalu lintas ke beberapa server backend, yang meningkatkan ketersediaan dan kinerja aplikasi.

4. **Cache**: Nginx dapat digunakan untuk caching konten, yang mengurangi beban pada server backend dan mempercepat waktu respons untuk pengguna.

5. **FastCGI, uWSGI, dan SCGI**: Nginx mendukung protokol-protokol ini untuk berkomunikasi dengan aplikasi server seperti aplikasi berbasis PHP, Python, dan lainnya.

6. **HTTP/2 dan gRPC**: Nginx mendukung protokol modern seperti HTTP/2 dan gRPC yang meningkatkan efisiensi komunikasi antara klien dan server.

Nginx sangat populer dalam lingkungan web modern karena kemampuannya untuk menangani jumlah koneksi yang sangat besar dengan penggunaan sumber daya yang minimal, menjadikannya pilihan utama untuk banyak situs web besar dan layanan online.

