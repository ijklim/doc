# Laravel Eloquent Query Builder Commands

* Documentation: https://laravel.com/docs/8.x/queries

```php
// Find by primary key `id`
\App\Models\User::find(8)->toArray();

// Get random data
\App\Models\Role::inRandomOrder()->first();

// Field selection
\App\Models\User::select('id', 'email')->get();
// Using addSelect and \DB::raw to add custom select fields
\App\Models\User::select('role_id')->addSelect(\DB::raw('UPPER(name) AS uname'))->first();

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

// Retrieve data with relationship count
\App\Models\Role::withCount('users')->get()->toArray();

// Append accessor `full_name` on demand using `append()` instead of `$append`
\App\Models\User::all()->append('full_name');


// Load relationship after retrieval
$role = \App\Models\Role::find(1);
$role->load('users');
// Use `refresh()` to reload relationship, useful if users.role_id has changed
$role->refresh();


// WhereHas
$userName = 'Ivan';
$role = \App\Models\Role::with('users');
$role->whereHas('users', function ($query) use ($userName) {
  $query->where('name', 'like', "%$userName%");
});
$role->get();

// Raw query
\App\Models\Role::with('users')->toSql();
```