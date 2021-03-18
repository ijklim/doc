# PHPUnit Assertions

* PHPUnit Doc: https://phpunit.readthedocs.io/en/9.5/assertions.html

* Laravel Testing Doc: https://laravel.com/docs/8.x/testing

* HTTP Test Doc: https://laravel.com/docs/8.x/http-tests

* Database Test Doc: https://laravel.com/docs/8.x/database-testing

```php
$this->assertDatabaseHas('users', ['name' => 'Jane Doe']);
$this->assertContains(8, [1, 2, 3]);

$this->assertFalse($variable);
$this->assertTrue($variable);
$this->assertEquals('TN', $region);
```
