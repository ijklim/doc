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

* *Important* Set `.env::SESSION_DOMAIN=dev-admin.askthelawyers.com`, domain must be the same as the actual domain showing the login page

* To verify whether session is behaving normally, `_token` in Debugbar Session tab should remain the same with page refresh

* Quite likely exception is also thrown 'CSRF token mismatch.'

* Checking request header, 'x-xsrf-token' header should be sent

* Clear cache of browser

* Clear all related cookies

  * Firefox: Click on lock left of url, select `Clear Cookies and Site Data...`

  * Chrome: Click on lock left of url, select `Cookies...`

  * Edge: Click on lock left of url, select `Cookies...`