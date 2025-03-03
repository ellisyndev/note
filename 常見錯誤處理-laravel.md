# 404 nginx
sudo chown -R www-data:www-data storage
sudo chmod -R ugo+rw storage
sudo chmod -R 775 storage
sudo chmod -R 755 storage/app
sudo chmod -R 775 storage bootstrap/cache

php artisan storage:link
sudo chmod -R 775 storage
sudo chmod -R a+rw storage
php artisan cache:clear
php artisan config:clear
php artisan config:cache

# 405
in App\Providers\AppServiceProvider;
增加
public function boot(): void
{
if (env('FORCE_HTTPS',false)) {
\Illuminate\Support\Facades\URL::forceScheme('https');
}
}

# 401
in App\Http\Middleware\TrustProxies
增加 protected $proxies = '*';

# 500
修改圖片權限
sudo chmod -R 775 storage/app

# 521
Starting base-cms_php-fpm_1 ... done
Starting base-cms_laravel-horizon_1 ... done
Starting base-cms_nginx_1           ... done
三個停止再重啟

# 413 422
因為本機使用php artisan serve

0.所以先使用
Route::get('/', function () {
dd(phpinfo());
});

1.查看目前設定，確認是否有正確設定到

2.如果沒有先確認設定檔位置
Configuration File (php.ini) Path

ex: /opt/homebrew/etc/php/8.2
 3.設定local php.ini
改
upload_max_filesize post_max_size

# database不能連
sail down --volumes
sail up -d

sail down
sail build --no-cache
sail up
php artisan config:clear
sail artisan migrate