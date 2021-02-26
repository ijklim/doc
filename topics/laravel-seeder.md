# Laravel Migration Script Methods

* Migration Doc: https://laravel.com/docs/8.x/seeding

* Command to create seeder script: `php artisan make:seeder RegionSeeder`

```php
namespace Database\Seeders;

use Illuminate\Database\Seeder;

class RegionSeeder extends Seeder
{
    public function run()
    {
        \DB::statement('SET FOREIGN_KEY_CHECKS=0');
        \App\Models\Region::truncate();
        \DB::statement('SET FOREIGN_KEY_CHECKS=1');

        $seeds = [
            ['Alabama', 'AL'],
            ['Alaska', 'AK'],
        ];

        foreach ($seeds as $seed) {
            \App\Models\Region::insert(self::addFieldNames($seed));
        }
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