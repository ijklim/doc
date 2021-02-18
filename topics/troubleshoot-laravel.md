# Laravel Troubleshooting Guide


## Can't write to /storage/logs/laravel.log

* Change permission of folder `/storage/logs`

  ```sh
  sudo chmod -R 777 /var/www/<name_of_repo>/storage
  ```


## Error 'The /var/www/<name_of_repo>/bootstrap/cache directory must be present and writable.'

* Set permission

  ```sh
  sudo chmod -R 755 /var/www/<name_of_repo>/bootstrap/cache
  ```


### The server requested authentication method unknown to the client

* php version 7.4+ is required, 7.3 produces that error


### Error '419 | Page Expired' during login (not solved yet)

* Ref: https://stackoverflow.com/questions/57766042/419-page-expired-laravel-5-8-after-login

* Check permission

  ```sh
  ls -la /var/www/admin.askthelawyers.com/bootstrap
  ls -la /var/www/admin.askthelawyers.com/bootstrap/cache
  chmod -R 777 /var/www/admin.askthelawyers.com/bootstrap/cache # Does not solve

  # Compare
  ls -la /var/www/atl_public_web2021/bootstrap

  ```