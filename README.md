# Simple PHP SSO integration for Laravel

<p align="center"><img src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>


This package based on [Simple PHP SSO skeleton](https://github.com/zefy/php-simple-sso) package and made suitable for Laravel framework.
### Requirements
* Laravel 5.5+
* PHP 7.1+

### Words meanings
* ***SSO*** - Single Sign-On.
* ***Server*** - page which works as SSO server, handles authentications, stores all sessions data.
* ***Broker*** - your page which is used visited by clients/users.
* ***Client/User*** - your every visitor.

### How it works?
Client visits Broker and unique token is generated. When new token is generated we need to attach Client session to his session in Broker so he will be redirected to Server and back to Broker so new session in Server will be created and associated with Client session in Broker's page. When Client visits other Broker same steps will be done except that when Client will be redirected to Server he already use his old session and same session id which associated with Broker#1.

# Installation
### Server
Install this package using composer.
```shell
composer require zefy/laravel-sso
```

Copy config file to Laravel project `config/` folder.
```shell
php artisan vendor:publish --provider="Zefy\LaravelSSO\SSOServiceProvider"
```

Create table where all brokers will be saved.
```shell
php artisan migrate --path=vendor/zefy/laravel-sso/database/migrations
```

Now you should create new brokers in your database at table named `brokers`.

### Broker
Install this package using composer.
```shell
composer require zefy/laravel-sso
```

Copy config file to Laravel project `config/` folder.
```shell
php artisan vendor:publish --provider="Zefy\LaravelSSO\SSOServiceProvider"
```

Change `type` value in `config/laravel-sso.php` file from `server`
 to `broker`.
 Set 3 new options in your `.env` file:
 ```shell
 SSO_SERVER_URL=
 SSO_BROKER_NAME=
 SSO_BROKER_SECRET=
 ```
 `SSO_SERVER_URL` is your server's http url without trailing slash (for example: https://server.test). `SSO_BROKER_NAME` and `SSO_BROKER_SECRET` must be data which exists in your server's `brokers` table.
 
 Example `.env` options:
  ```shell
 SSO_SERVER_URL=https://server.test
 SSO_BROKER_NAME=site1
 SSO_BROKER_SECRET=892asjdajsdksja74jh38kljk2929023
 ```
 
 For other brokers everything is the same.