# Laravel Eloquent Query Builder Commands

* Documentation: https://laravel.com/docs/8.x/queries

```php
// Find by primary key `id`
\App\Models\User::find(8)->toArray();

// Where Null
\App\Models\User::whereNull('user_name')->get()->toArray();
```