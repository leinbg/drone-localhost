drone on localhost
==================
test drone server and agent on localhost, need ngrok to publish localhost

## how to use
1. install ngrok and forward localhost:80

    ```
    npm install
    node_modules/ngrok/bin/ngrok http 80
    ```

2. add bitbucket oauth comsumer with ngrok url:

    |parameter          |value                          |
    |-------------------|-------------------------------|
    |callback url       |http://12345.ngrok.io/authorize|
    |account            |read, email                    |
    |team membership    |read                           |
    |repositories       |read                           |
    |webhooks           |read and write                 |

3. copy key and secret to `drone-up` script, then run

    ```
    drone-up
    ```

## examples
laravel ci .drone.yml

```
pipeline:
    composer:
        image: composer/composer
        commands:
            - composer install --prefer-source

    test:
        image: php
        commands:
            - mv .test.env .env
            - ls -lah
            - touch database/database.sqlite
            - php artisan migrate
            - vendor/bin/phpunit

branches: master
```
