# Laravel Eloquent Query Builder Commands

* Documentation: https://laravel.com/docs/8.x/queries

```php
// Find by primary key `id`
\App\Models\User::find(8)->toArray();

// Get random data
\App\Models\Role::inRandomOrder()->first();

// Field selection
\App\Models\User::select('id', 'email')->get();

// Retrieve a single row
\App\Models\User::where('name', 'John')->first();

// Where Like
\App\Models\User::where('name', 'like', 'T%')->get();

// Null (whereNull)
\App\Models\User::whereNull('name')->get()->toArray();

// In (whereIn), Not In (whereNotIn)
\App\Models\User::whereIn('name', ['Jon', 'Skye'])->get()->toArray();

// Custom where clause
\App\Models\User::whereRaw('id > IF(name = "Smith", 10, 2)')->get()->toArray();

// Retrieve column data (name), with optional key field (id)
\App\Models\User::pluck('name', 'id')->all();

// Order By
\App\Models\User::orderBy('name', 'DESC')->get();

// With relationship
\App\Models\Role::with('users')->find(1);

// Load relationship after retrieval
$role = \App\Models\Role::find(1);
$role->load('users');

// WhereHas
$userName = 'Ivan';
$role = \App\Models\Role::with('users');
$role->whereHas('users', function ($query) use ($userName) {
  $query->where('name', 'like', "%$userName%");
});
$role->get();
```