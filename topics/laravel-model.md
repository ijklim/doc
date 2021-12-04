# Laravel Model

* Doc: https://laravel.com/docs/8.x/eloquent

* Model Class: https://laravel.com/api/8.x/Illuminate/Database/Eloquent/Model.html

* Validation: https://laravel.com/docs/8.x/validation

* Tables are defined in repo `/web/laravel/laravel-doc`

* Command to create migration script with model: `php artisan make:model MySample -m`

  * Add `-f` to create a factory class as well

* To create a model instance using factory: `\App\Post::factory()->make()`;

  * Create and save in table: `\App\Post::factory()->create()`

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


    // Post has many comments
    public function comments()
    {
        return $this->hasMany(
            Comment::class,
            'post_id',                      // Foreign key to Post in Comment
            'id'                            // Primary key in Post
        );
    }

    // Post has one post_info
    public function postInfo()
    {
        return $this->hasOne(
            PostInfo::class,
            'post_id',                      // Foreign key to Post in PostInfo
            'id'                            // Primary key in Post
        );
    }

    // Post has many post_info_details through post_info
    public function postInfoDetails()
    {
        return $this->hasManyThrough(
            PostInfoDetail::class,          // Final model
            PostInfo::class,                // Intermediate model
            'post_id',                      // Foreign key to Post on PostInfo
            'post_info_id',                 // Foreign key to PostInfo on PostInfoDetail
            'id',                           // Primary key on Post
            'id',                           // Primary key on PostInfo
        );
    }

    // Many to many, e.g. post has many tags, tags shared by many posts
    public function tags()
    {
        return $this->belongsToMany(
            \App\Models\Tag::class,
            'post_tag',                     // Intermediate pivot table
            'post_id',                      // Foreign key to Post in table `post_tag`
            'tag_id'                        // Foreign key to Tag in table `post_tag`
        );
    }

    // Post has one user
    public function user()
    {
        return $this->belongsTo(
            User::class,
            'user_id',                      // Foreign key to User in Post
            'id'                            // Primary key in User
        );
    }
}
```

# Creation through relationships

```php
// 1 to many
$post->postInfoDetails()->create[
    'notes' => 'Very important notes',
];
```