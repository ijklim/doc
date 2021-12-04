# Laravel Helpers

* HTTP Requests: https://laravel.com/docs/8.x/requests

```php
# Date and Time
echo now()->addDays(8);
echo now()->addMinutes(8)->diffInMinutes();

# String
$s = 'this-is ALong_sentencE';
echo \Str::headline($s);
echo \Str::studlyWords($s);
echo \Str::of('<b>this is bold</b>')->stripTags();

```