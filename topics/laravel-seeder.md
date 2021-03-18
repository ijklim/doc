# Laravel Seeder

* Migration Doc: https://laravel.com/docs/8.x/seeding

* Command to create seeder script: `php artisan make:seeder RegionSeeder`

* To run all seeders defined in `database/seeders/DatabaseSeeder.php`: `php artisan db:seed`

* To run individual seeder: `php artisan db:seed --class=RegionSeeder`

* Create trait `app\Http\Traits\SeederTrait.php`

```php
namespace App\Http\Traits;

trait SeederTrait
{
    /**
     * Extract table name from seeder class name
     */
    private function getTableName()
    {
        // Remove 'Seeder' from back of class name, add 's' to the end
        $className = basename(__CLASS__);
        return \Str::snake(substr($className, 0, strlen($className) - strlen('Seeder'))) . 's';
    }

    /**
     * Delete all data from a table
     */
    private function deleteTable()
    {
        \DB::delete("DELETE FROM " . $this->getTableName());
        \DB::statement("ALTER TABLE " . $this->getTableName() . " AUTO_INCREMENT = 1;");
    }
}
```

```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;

class RegionSeeder extends Seeder
{
    public function run()
    {
        echo "=== " . basename(__CLASS__) . " ===\n";

        echo "• Clearing old data\n";
        $this->deleteTable();

        $seeds = [
            ['Alabama', 'AL'],
            ['Alaska', 'AK'],
        ];

        foreach ($seeds as $seed) {
            \App\Models\Region::insert(self::addFieldNames($seed));
        }
        echo "• Populated Regions: " . count($seeds) . "\n";

    }

    public static function addFieldNames($dataArray)
    {
        $fieldNames = [
            'region_name',
            'region_code',
        ];
        return array_combine($fieldNames, $dataArray);
    }
}
```

```php
// Color output
$this->command->getOutput()->writeln("<comment>Seeder \<comment>!</comment>");
$this->command->getOutput()->writeln("<error>Seeder \<error>!</error>");
$this->command->getOutput()->writeln("<info>Seeder \<info>!</info>");
$this->command->getOutput()->writeln("<question>Seeder \<question>!</question>");
```