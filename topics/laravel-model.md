# Laravel Model

* Doc: https://laravel.com/docs/8.x/eloquent

* Command to create migration script with model: `php artisan make:model MySample -m`

  * Add `-f` to create a factory class as well

```php
namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    // Allows use of Post::factory()->make()
    // `database\factories\PostFactory.php` must be present
    use HasFactory;

    /**
     * The primary key associated with the table.
     *
     * @var string
     */
    protected $primaryKey = 'post_id';

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'user_id',
        'content',
    ];
}
```