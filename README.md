# docker-laravel

Laravelプロジェクト

## Docker

### 設定ファイル
```bash
$ cp .env.example .env
```

### build & up
```bash
$ docker-compose up -d
```

### コンテナ接続
```bash
$ docker-compose exec web bash
```

## Laravelプロジェクト

https://github.com/Vuedo/vuedo

### Installation
```bash
$ cp .env.example .env
$ composer install
$ npm install
$ php artisan key:generate
$ php artisan migrate
$ php artisan db:seed
$ npm run dev
```

### サーバ起動
```bash
$ php artisan serve
```

* WEB
http://127.0.0.1
http://127.0.0.1/dashboard

* phpMyAdmin
http://127.0.0.1/8080

接続できなければDockerのIPを確認
http://192.168.99.100