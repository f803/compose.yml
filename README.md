# ![Docker](https://img.icons8.com/?size=35&id=cdYUlRaag9G9&format=png) Как запустить

`git clone https://github.com/f803/compose.yml.git`   

### и выполнить  
` docker compose up `  

![Script](https://img.icons8.com/?size=25&id=37927&format=png) [Скрипт используемый в **Wordpress**](https://raw.githubusercontent.com/f803/test/refs/heads/main/script.sh)



## Сервисы

### ![Nginx](https://img.icons8.com/?size=30&id=t2x6DtCn5Zzx&format=png) **nginx**
- Образ: `nginx:stable-alpine3.20-perl`
- Открывает порт 80 для веб-доступа.
- Связан с сетью **nginx_wordpress**, чтобы взаимодействовать с **WordPress**.
- Обеспечивает выход в интернет для контейнера **WordPress**.

### ![Wordpress](https://img.icons8.com/?size=30&id=v9uZbuVoWleB&format=png) **wordpress**
- Образ: `wordpress:6.7.0-php8.1-fpm`
- Работает с PHP-FPM.
- Связан с сетями **nginx_wordpress** и **wordpress_db**.
- Зависит от базы данных **MariaDB**.

### ![Redis](https://img.icons8.com/?size=30&id=RMtSR4z10z2l&format=png) **redis**
- Образ: `redis:alpine3.20`
- Предоставляет кэширование для **WordPress**.
- Связан с сетью **wordpress_db**.

### ![MariaDB](https://img.icons8.com/?size=30&id=DakakaPez2uy&format=png) **db (MariaDB)**
- Образ: `mariadb:11.5.2`
- База данных MariaDB для **WordPress**.
- Связан с сетью **wordpress_db**.

## ![Сети](https://img.icons8.com/?size=30&id=59368&format=png) Сети

- **nginx_wordpress**: 
  - Связана с **nginx** и **WordPress**, а также обеспечивает выход в интернет для WordPress.
  
- **wordpress_db**: 
  - Связана с **WordPress**, **Redis** и **MariaDB** для внутреннего общения между сервисами.

## Томa

- **db_data**: Персистентное хранилище для данных MariaDB.

## Обзор конфигурации

- **WordPress** настроен на использование **Redis** для кэширования и **MariaDB** для базы данных.
- **Nginx** действует как реверс-прокси для **WordPress**, обрабатывая PHP-запросы через FastCGI.
