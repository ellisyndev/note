# laravel 11 + filament v3

## 建立專案
curl -s "https://laravel.build/example-app" | bash
cd example-app

## 改配置
.env
APP_NAME=example-app
APP_TIMEZONE=Asia/Taipei
LOG_CHANNEL=daily
APP_LOCALE=zh_TW
DB_DATABASE=example-app

## 跑起來
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
sail up -d

## 資料庫連線
User->sail
Password->password
Database->專案名

## 安裝 filament
composer require filament/filament="3.2.57" -W
php artisan filament:install --panels
php artisan make:filament-user

## mac php 版本錯誤
brew list php
brew link --overwrite --force php@8.2

## 對建立的容器進行調整
可以將 sail 的 docker-compose.yml 產出來。
就會多一個 docker 資料夾
php artisan sail:publish
sail build --no-cache