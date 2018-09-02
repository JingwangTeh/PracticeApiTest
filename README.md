# PracticeApiTest
reminder: 
- Run command 'composer update && composer install'
- Create .env file from .env.example
  ~ set APP_ENV=prod
  ~ set APP_KEY by using 'php artisan key:generate'
- Go to Configuration -> Software Configuration -> Set Document root: '/public'

- Add database to Data Tier

- Dynamically set database values in config/database.php
	define('RDS_HOSTNAME', $_SERVER['RDS_HOSTNAME']);
	define('RDS_USERNAME', $_SERVER['RDS_USERNAME']);
	define('RDS_PASSWORD', $_SERVER['RDS_PASSWORD']);
	define('RDS_DB_NAME', $_SERVER['RDS_DB_NAME']);

	'mysql' => [
		...
		'host' => RDS_HOSTNAME,
		'database' => RDS_DB_NAME,
		'username' => RDS_USERNAME,
		'password' => RDS_PASSWORD,
		...

- Overwrite default database version laravel assumes,
  in app/Providers/AppServiceProvider.php
	
	use Schema;
 
	public function boot()
	{
		Schema::defaultStringLength(191);
	}
	
- Create folder '.ebextensions' and create file 'init.config', 
  which will run by aws beanstalk every time a new app version is deployed
- Insert into init.config, which will run migration:
  container_commands:
    01initdb:
		command: "php artisan migrate"

- if MAC_OSX, remember to remove the folder __MACOSX