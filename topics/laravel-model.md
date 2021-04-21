# Laravel Model

* Doc: https://laravel.com/docs/8.x/eloquent

* Model Class: https://laravel.com/api/8.x/Illuminate/Database/Eloquent/Model.html

* Validation: https://laravel.com/docs/8.x/validation

* Command to create migration script with model: `php artisan make:model MySample -m`

  * Add `-f` to create a factory class as well

```php
namespace App\Models;

class Post extends \Illuminate\Database\Eloquent\Model
{
    // Allows use of Post::factory()->make()
    // `database\factories\PostFactory.php` must be present
    use \Illuminate\Database\Eloquent\Factories\HasFactory;

    /**
     * The primary key associated with the table.
     *
     * @var string
     */
    protected $primaryKey = 'post_id';

    /**
     * Whether primary key auto increment. Affects primary key field value after `->save()`
     *
     * @var boolean
     */
    public $incrementing = false;

    /**
     * Table has no timestamp fields `created_at` and `updated_at`
     */
    public $timestamps = false;

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'user_id',
        'content',
    ];

    /**
     * The attributes that are not mass assignable.
     * Note: $guarded is the reverse of $fillable, use only one
     *
     * @var array
     */
    protected $guarded = [];

    // Post has one user
    public function user()
    {
        return $this->belongsTo(\App\Models\User::class, 'user_id');
    }

    // Post has many comments
    public function comments()
    {
        return $this->hasMany(\App\Models\Comment::class, 'comment_id');
    }

    // Many to many, e.g. user has many roles, roles shared by many users
    public function roles()
    {
        return $this->belongsToMany(\App\Models\Role::class);
    }
}
```