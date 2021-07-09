# Laravel Artisan Commands

```sh
# Show available routes
php artisan route:list

# Create migration script
php artisan make:migration create_posts_table

# Create seeder script
php artisan make:seeder UserSeeder

# Create model script
php artisan make:model Role

# Run migration script
php artisan migrate
## Delete all tables and run all migration scripts
php artisan migrate:fresh
## With seeding
php artisan migrate:fresh --seed
```