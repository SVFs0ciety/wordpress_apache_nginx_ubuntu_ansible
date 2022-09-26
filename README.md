Запуск основного файла - playbook.yml
playbook.yml автоматически развернет nginx + php 81 + php-fpm + mysql + csf + maldet + lynis + wordpress
В папке configs содержатся конфигурационные файлы nginx и csf

Создание базы данных:
- В файле wordpress.yml содержатся строки 

cmd: mysql -u root -pmEsh0chek -e "CREATE DATABASE wpdb; CREATE USER 'linux'@localhost IDENTIFIED BY 'mEsh0chek'; GRANT ALL PRIVILEGES ON wpdb.* TO linux@localhost IDENTIFIED BY 'mEsh0chek'; FLUSH PRIVILEGES;"
Эта строка отвечает за создание пользователя и бд.

Эти строки отвечают за конфигурационный файл wp-config.php,отвечающий за подклюючение к БД.

 with_items:
        - {'regexp': "define\\( 'DB_NAME', '(.)+' \\);", 'line': "define( 'DB_NAME', 'wpdb' );"}
        - {'regexp': "define\\( 'DB_USER', '(.)+' \\);", 'line': "define( 'DB_USER', 'linux' );"}
        - {'regexp': "define\\( 'DB_PASSWORD', '(.)+' \\);", 'line': "define( 'DB_PASSWORD', 'mEsh0chek' );"}
