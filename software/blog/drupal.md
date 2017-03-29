https://www.drupal.org/documentation/install/create-database


$ sudo cp ~/下载/drupal*.tar.gz /usr/share/nginx/html/drupal*.tar.gz

$ sudo tar zxvf drupal*.tar.gz
$ sudo rm  drupal*.tar.gz
$ sudo mv drupal-8.0.5 drupal
$ mysql -u root -p
$ sudo vim create_database.sql
$ source create_db.sql

$ http://localhost/drupal/
$ sudo mkdir /usr/share/nginx/html/drupal/default/files/translations
$ sudo chmod a+w default/

fail....
