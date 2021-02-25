# Laravel Migration Script Methods

* Migration Doc: https://laravel.com/docs/8.x/migrations

* Model Doc: https://laravel.com/docs/8.x/eloquent

* Command to create migration script with model: `php artisan make:model MySample -m`

  * Add `-f` to create a factory class as well

```php
// === Table Creation ===
class CreateMySamplesTable extends Migration
{
    const TABLE_NAME = 'my_samples';

    public function up()
    {
        Schema::dropIfExists(self::TABLE_NAME);

        Schema::create(self::TABLE_NAME, function (Blueprint $table) {
            $table->increments(substr(self::TABLE_NAME, 0, -1) . '_id');
            $table->foreignId('import_batch_id')->constrained()->onDelete('cascade');
            $table->foreign('user_id')->references('id')->on('users');
            $table->boolean('completed')->default(false);
            $table->string('name', 30);
            $table->string('email', 100)->index();
            $table->string('sample_file', 10)->unique();
            $table->text('description');
            $table->longText('notes');
            $table->unsignedTinyInteger('level');
            $table->unsignedDecimal('taxes', 8, 2);
            $table->string('region', 10)->nullable()->comment = 'Nice';
            $table->timestamp('email_verified_at')->nullable();
        });

        // Or
        Schema::create(self::TABLE_NAME, function (Blueprint $table) {
            $table->integer('post_id');
            $table->foreign('post_id')->references('id')->on('posts');
            $table->integer('tag_id');
            $table->foreign('tag_id')->references('id')->on('tags');

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
        Schema::dropIfExists(self::TABLE_NAME);
    }
}
```