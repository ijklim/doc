# Laravel Migration Script Methods

* Migration Doc: https://laravel.com/docs/8.x/migrations

* Command to create migration script: `php artisan make:migration create_my_samples_table`

* To re-create database from scratch: `php artisan migrate:refresh`

* Create trait `app\Http\Traits\MigrationTrait.php`

```php
namespace App\Http\Traits;

trait MigrationTrait
{
    /**
     * Extract table name from Create Table migration class name
     */
    private function getTableName()
    {
        // Remove 'Create' from front and 'Table' at back of class name
        return \Str::snake(substr(__CLASS__, strlen('Create'), strlen(__CLASS__) - strlen('CreateTable')));
    }

    /**
     * Add table level comment
     */
    private function addTableComment($comment)
    {
        $sql = "
            ALTER TABLE " . $this->getTableName() . "
            COMMENT '$comment';
        ";
        \DB::unprepared($sql);
    }
}
```

```php
// === Table Creation ===
class CreateMySamplesTable extends Migration
{
    use App\Http\Traits\MigrationTrait;

    public function up()
    {
        $this->down();

        Schema::create($this->getTableName(), function (Blueprint $table) {
            $table->increments(\Str::singular($this->getTableName()) . '_id');

            $table->boolean('completed')->default(false);

            $table->string('name', 30)->index();
            $table->string('email', 100)->unique();
            $table->text('description');
            $table->longText('notes');

            $table->unsignedTinyInteger('level')->nullable()->comment = 'Importance of article';
            $table->unsignedDecimal('taxes', 8, 2);

            $table->timestamp('email_verified_at')->nullable();
            $table->date('date_scheduled');
        });

        // Other variations
        Schema::create($this->getTableName(), function (Blueprint $table) {
            $table->unsignedBigInteger('post_id');
            $table->foreign('post_id')->references('id')->on('posts');

            $table->integer('tag_id');
            $table
                ->foreign('tag_id')
                ->references('tag_id')
                ->on('tags')
                ->onUpdate('cascade')
                ->onDelete('cascade');

            // Alternatives
            $table->foreignId('user_id')->constrained();
            $table->foreignId('user_id')->constrained('users');
            $table->foreignId('user_id')->constrained()->onUpdate('cascade')->onDelete('cascade');

            $table->primary(['zip_code', 'tag_id']);
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists($this->getTableName());

        $table->dropForeign('posts_user_id_foreign');
        $table->dropForeign(['user_id']);

        Schema::enableForeignKeyConstraints();
        Schema::disableForeignKeyConstraints();
    }
}
```