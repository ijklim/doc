# Laravel Collection Methods

* Documentation: https://laravel.com/docs/8.x/collections

```php
$results = collect(['apple', 'banana', 'cherry'])
  ->map(function ($val) {
      return strtoupper($val);
  })
  ->reject(function ($val) {
      return $val > 'B';
  })
  ->toArray();

print_r($results);
```