
## Deployment

Tahapan Menjalankan

Cloning terlebih dahulu
```bash
  git clone https://github.com/nvrthink/containerization.git
```

```bash
  cd containerization
```

Build image nginx
```bash
  podman build -t my-nginx-image ./nginx/
```

Build image php
```bash
  podman build -t php ./php_code
```
Pull image mariadb
```bash
  podman pull mariadb
```

Membuat pod dengan nama webservice
```bash
  podman pod create --name webservice -p 8080:80
```
Menjalankan container untuk nginx 
```bash
podman run -d --name nginx —pod webservice -v ./php_code:/usr/share/nginx/html/ localhost/my_nginx
```
Menjalankan container untuk php 
```bash
podman run -d --name php –pod webservice -v ./php_code:/var/www/html/  localhost/php_web
```
Menjalankan container untuk mariadb
```bash
podman run -d --name my-db  --pod webservice -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mariadb mariadb
```

Cek apakah semua sudah berjalan dengan command 
```bash
podman ps
````
![App Screenshot](https://raw.githubusercontent.com/nvrthink/containerization/master/podman_ps.png)

## Hasil Uji
![App Screenshot](https://raw.githubusercontent.com/nvrthink/containerization/master/halaman_login.png)
![App Screenshot](https://raw.githubusercontent.com/nvrthink/containerization/master/registrasi_sukses.png)


