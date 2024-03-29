# Laravel Troubleshooting Guide


## Can't write to /storage/logs/laravel.log

* Change permission of folder `/storage/logs`

  ```sh
  repoRoot=$(pwd)
  sudo chmod -R 777 $repoRoot/storage
  ```

* Note: 755 or 775 do not work


## Error 'The /var/www/<name_of_repo>/bootstrap/cache directory must be present and writable.'

* Set permission

  ```sh
  sudo chmod -R 755 /var/www/<name_of_repo>/bootstrap/cache
  ```


## The server requested authentication method unknown to the client

* php version 7.4+ is required, 7.3 produces that error


## Error '419 | Page Expired' during login (possible solutions)

* *Important* Set `.env::SESSION_DOMAIN` and `.env::APP_URL`, domain must be the same as the actual domain showing the login page

  * e.g. `SESSION_DOMAIN=dev-admin.askthelawyers.com`

* To verify whether session is behaving normally, `_token` in Debugbar Session tab should remain the same with page refresh

* Cause: Quite likely exception is also thrown 'CSRF token mismatch.'

* Checking request header, 'x-xsrf-token' header should be sent

* Clear cache of browser

* Clear all related cookies

  * Firefox: Click on lock left of url, select `Clear Cookies and Site Data...`

  * Chrome: Click on lock left of url, select `Cookies...`

  * Edge: Click on lock left of url, select `Cookies...`

## Error 'Swift_TransportException Connection could not be established with host mailhog :stream_socket_client(): php_network_getaddresses: getaddrinfo failed: No such host is known.'

* Need to configure `MAIL_*` settings in `.env` file

## Warning 'You are running the esm-bundler build of Vue. It is recommended to configure your bundler to explicitly replace feature flag globals with boolean literals to get proper tree-shaking in the final bundle.'

* Configure `webpack.config.js`

  ```js
  const path = require('path');
  const webpack = require('webpack');

  module.exports = {
      resolve: {
          alias: {
              '@': path.resolve('resources/js'),
          },
      },
      plugins: [
          new webpack.DefinePlugin({
              __VUE_OPTIONS_API__: true,
              __VUE_PROD_DEVTOOLS__: true,
          }),
      ],
  };
  ```

## Warning 'DevTools failed to load SourceMap: Could not load content for...'

* Configure `webpack.mix.js`

  ```js
  mix.js('resources/js/app.js', 'public/js').sourceMaps();
  ```

## [Aws\Exception\CredentialsException] Error retrieving credentials from the instance profile metadata service.

* `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` in `.env` have not been set up or they are invalid

## PHP Fatal error:  Allowed memory size of 134217728 bytes exhausted (tried to allocate 20480 bytes)

* Occurs when attempting to run `php artisan route:list`

* Increase `memory_limit` setting in `php.ini`, use `phpinfo()` to determine where the `php.ini` file is located

* Command line php and the one used by Laravel might be different, if using xampp, might need to specify path (e.g. `c:/xampp/php-7.4/php artisan route:list`)


## Target class [Database\Seeders\ConfigurationSeeder] does not exist.

* Configure `composer.json`

  ```json
  "autoload": {
    "psr-4": {
      "App\\": "app/",
      "Database\\Seeders\\": "database/seeders/"
    }
  },
  ```

* Run `composer dump-autoload`