# Laravel Collection Methods

* Documentation: https://laravel.com/docs/8.x/collections

```php
$results = collect(['apple', 'banana', 'cherry'])
  ->map(function ($val) {
      return strtoupper($val);
  })
  ->reject(function ($val) {
      return $val > 'B';
  });

// Convert to array
$a = $results->toArray();
// Get only fixed number of rows
$b = $results->take(2);
//

// Another example
$results = collect(['php', 'vue', 'laravel'])->random(2)->values()->all();

// hasAny
echo collect(['first' => 'Hello', 'second' => 'World'])->hasAny(['first', 'fourth']);   // Match key only, case sensitive

// Search in collection
\App\Models\User::all()->firstWhere('name', 'Ivan Lim');
```