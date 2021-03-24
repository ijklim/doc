# Laravel Gate Methods

* Authorization: https://laravel.com/docs/8.x/authorization

## Definition

* In `app/Providers/AuthServiceProvider.php`

```php
public function boot()
{
    $this->registerPolicies();

    Gate::define('update-post', function (User $user, Post $post) {
        return $user->id === $post->user_id;

        // or detailed response with error message
        return $user->isAdmin
            ? \Illuminate\Auth\Access\Response::allow()
            : \Illuminate\Auth\Access\Response::deny('You must be an administrator.');

    });

    // Runs before all other authorization checks
    Gate::before(function ($user, $ability) {
    if ($user->isAdministrator()) {
        return true;
    }

    // Runs after all other authorization checks
    Gate::after(function ($user, $ability, $result, $arguments) {
    if ($user->isAdministrator()) {
        return true;
    }
}
```

## Authorization

```php
Gate::allows('update-post', $post);
Gate::denies('update-post', $post);

// Checking for user other than the currently authenticated user
Gate::forUser($user)->allows('update-post', $post));
$request->user()->can('update', $post);
$request->user()->cannot('create', Post::class);  // Does not require model

Gate::any(['update-post', 'delete-post'], $post);
Gate::none(['update-post', 'delete-post'], $post);

// Automatically throw an Illuminate\Auth\Access\AuthorizationException
Gate::authorize('update-post', $post);

// Array as second argument
Gate::check('create-post', [$category, $pinned]);

// Using inspect to get response
$response = Gate::inspect('edit-settings');
$response->allowed();
echo $response->message();

```

## Policy

```sh
# Create empty policy
php artisan make:policy PostPolicy

# Create policy for a model
php artisan make:policy PostPolicy --model=Post
```

* Register policy in `app/Providers/AuthServiceProvider.php`

```php
// Will be auto discovered if PostPolicy.php is in `app/Policies` or `app/Models/Policies`
protected $policies = [
    \App\Models\Post::class => \App\Policies\PostPolicy::class,
];
```

* Policy definition

```php
class PostPolicy
{
    /**
     * Determine if the given post can be updated by the user.
     *
     * @param  \App\Models\User  $user
     * @param  \App\Models\Post  $post
     * @return bool
     */
    public function update(User $user, Post $post)
    {
        return $user->id === $post->user_id;
    }

    public function create(User $user)
    {
        return $user->role == 'writer';
    }
}
```