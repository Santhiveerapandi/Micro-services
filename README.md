# Install and Set Up Laravel with Docker Compose

Setting up Laravel in the local environment with Docker using the LEMP stack that includes: Nginx, MySQL, PHP, and phpMyAdmin.

## Why use Docker for Development

- [x] Consistent development environment for the entire team.
- [x] You don't need to install a bunch of language environments on your system.
- [x] You can use different versions of the same programming language.
- [x] Deployment is easy

## How to Install and Run the Project

1. ``` git clone https://github.com/Santhiveerapandi/Micro-services.git ```
2. ``` cd Micro-services ```

## Microservices are ProductService, OrderService.
1. ``` cd ProductService ```
1.1. ``` docker compose build ```
1.2. ``` docker compose up -d ```
1.3. ``` docker compose exec product_app composer install ```
1.4. Copy ```.env.example``` to ```.env```
1.5. ``` docker compose exec product_app php artisan migrate ```
1.6. You can see the project on ```127.0.0.1:8080```

2. ``` cd OrderService ```
2.1. ``` docker compose build ```
2.2. ``` docker compose up -d ```
2.3. ``` docker compose exec order_app composer install ```
2.4. Copy ```.env.example``` to ```.env```
2.5. ``` docker compose exec order_app php artisan migrate ```
2.6. You can see the project on ```127.0.0.1:8080```

## How to use MySQL as a database

1. Uncomment the MySQL configuration inside the ```docker-compose.yml``` including: ```db``` and ```phpMyAdmin```
2. Copy ```.env.example``` to ```.env```
3. Change ```DB_CONNECTION``` to ```mysql```
4. Change ```DB_PORT``` to ```3306```
5. Open the ```phpMyAdmin``` on ```127.0.0.1:3400```

## How to use PostgreSQL as a database

1. Uncomment the PostgreSQL configuration inside the ```docker-compose.yml``` including: ```db``` and ```pgamdin```
2. Copy ```.env.example``` to ```.env```
3. Change ```DB_CONNECTION``` to ```pgsql```
4. Change ```DB_PORT``` to ```5432```
5. Open the ```pgAdmin``` on ```127.0.0.1:5050```

## How to run Laravel Commands with Docker Compose

1. ```cd src```
2. ```docker-compose exec app php artisan {your command}``` 

## RabbitMQ Reference
https://github.com/vyuldashev/laravel-queue-rabbitmq

Both ProductService & OrderService
src/config/queue.php

```
    'connections' => [
        ...
        //RabbitMQ - Message Broker Helps to communicate two microservices (Ex, Product & Order Service)
        'rabbitmq' => [
    
            'driver' => 'rabbitmq',
            'queue' => env('RABBITMQ_QUEUE', 'default'),
            'connection' => PhpAmqpLib\Connection\AMQPLazyConnection::class,
            'hosts' => [
                [
                    'host' => env('RABBITMQ_HOST', '127.0.0.1'),
                    'port' => env('RABBITMQ_PORT', 5672),
                    'user' => env('RABBITMQ_USER', 'guest'),
                    'password' => env('RABBITMQ_PASSWORD', 'guest'),
                    'vhost' => env('RABBITMQ_VHOST', '/'),
                ],
            ],

            'options' => [
                'ssl_options' => [
                    'cafile' => env('RABBITMQ_SSL_CAFILE', null),
                    'local_cert' => env('RABBITMQ_SSL_LOCALCERT', null),
                    'local_key' => env('RABBITMQ_SSL_LOCALKEY', null),
                    'verify_peer' => env('RABBITMQ_SSL_VERIFY_PEER', true),
                    'passphrase' => env('RABBITMQ_SSL_PASSPHRASE', null),
                ],
                'queue' => [
                    'job' => \VladimirYuldashev\LaravelQueueRabbitMQ\Queue\Jobs\RabbitMQJob::class,
                ],
            ]
        ],
    ]
```

## RabbitMQ Instance creation
https://customer.cloudamqp.com
Login with Gmail


```docker network ls```

```docker network create shopping```

``` docker-compose build ```

``` docker-compose up -d ```

## Queue
1. ```docker compose exec product_app php artisan queue:work```
2. ```docker compose exec order_app php artisan queue:work```


## Medium

https://medium.com/@hanieasemi/setting-up-a-laravel-local-environment-with-docker-7541ae170daf

## YouTube 

https://www.youtube.com/watch?v=6ANYowpB910

https://www.youtube.com/watch?v=gZfCAIGsz_o
