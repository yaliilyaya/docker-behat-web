# docker-behat-web
docker container with behat + php-fpm7.1 + facebook web driver

Первичный план
разворачиваем через докер компосер

- container php-fpm7.1
    - composer
        - behat
        - phpunit
        - facebook webdriver
    - volume
        - dir test
- нельзя давать доступ к серверу
- container ssh
    - volume
        - dir test