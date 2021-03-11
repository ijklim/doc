# Laravel Database Methods

* Documentation: https://laravel.com/docs/8.x/database

```php
DB::beginTransaction();
DB::commit();
DB::rollBack();

DB::delete('DELETE FROM users WHERE email = ?', ['jon@example.com']);

DB::insert('INSERT INTO users (email) VALUES (?, ?)', ['Jon', 'jon@example.com']);

DB::select('SELECT * FROM users WHERE active = ?', [1]);

DB::statement("ALTER TABLE users AUTO_INCREMENT = 1");

DB::unprepared('ALTER TABLE users COMMENT "Internal Staff"');

DB::update('UPDATE users SET name = ? WHERE email = ?', ['Smith', 'jon@example.com']);

// Retrieve one row
$user = DB::table('users')->where('email', 'jon@example.com')->first();
```