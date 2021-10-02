# wordpress-docker

Anda dapat membuat file untuk langsung menjalankan script dalam satu command, atau bisa juga menjalankan secara terpisah. Saya akan berikan untuk menjalankan sekaligus dalam satu script.
1. Create file dengan nama wordpress-docker.sh
2. Open file dan Paste-kan script berikut ini:
#!/bin/sh
mkdir -p /home/bayu/shopee/db
sudo chown -R 27:27 /home/bayu/shopee/db
sudo semanage fcontext -a -t container_file_t '/home/bayu/shopee/db(/.*)?'
sudo restorecon -Rv /home/bayu/shopee/db

sudo docker run -d --name wpdb \
    -v /home/bayu/shopee/db:/var/lib/mysql/data \
    -p 3306:3306
    -e MYSQL_USER=user_shopee \
    -e MYSQL_PASSWORD=P4ssword! \
    -e MYSQL_DATABASE=wordpress \
    -e MYSQL_ROOT_PASSWORD=r00tP4ssword! \
    rhscl/mysql-57-rhel7

sudo docker run --name=wpweb \
-d -p 8080:80 \
-e WORDPRESS_DB_HOST=0.0.0.0:3306 \
-e WORDPRESS_DB_USER=user_shopee \
-e WORDPRESS_DB_PASSWORD=P4ssword! \
-e WORDPRESS_DB_NAME=wordpress \
wordpress

3. jalankan command berikut:
chmod +x  wordpress-docker.sh
./wordpress-docker.sh

(pastikan docker sudah terinstall pada device yang anda gunakan)

