# Docker - MariaDB + PhpMyAdmin


#### Files:
* docker-composer.yml


#### `docker-compose.yml`:
```yaml
version: "3.7"

services:


  # MariaDB
  # ----------------------------------------------------------------------
  mariadb:
    image:   'mariadb:10.4'
    restart: 'always'
    volumes: [ 'mariadb-data:/var/lib/mysql' ]
    environment:
      MYSQL_ROOT_PASSWORD: 'qwerty'
  # ----------------------------------------------------------------------


  # PhpMyAdmin
  # ----------------------------------------------------------------------
  phpmyadmin:
    image:      'phpmyadmin/phpmyadmin:latest'
    ports:      [ '3001:80' ]
    restart:    'always'
    depends_on: [ 'mariadb' ]
    environment:
      PMA_HOST:      'mariadb'
      PMA_PORT:      3306
      PMA_USER:      'root'
      PMA_PASSWORD:  'qwerty'
      UPLOAD_LIMIT:  '10G'
      PMA_ARBITRARY: 1
  # ----------------------------------------------------------------------


volumes:
  mariadb-data:
```
