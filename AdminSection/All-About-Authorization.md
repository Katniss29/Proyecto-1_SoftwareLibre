## All About Authorization

- Para este video optimizamos y eliminamos ciertas rutas que no se necesitan, se borra el middleware ya que no se utiliza, se agrega la autorización personalizanda usando `Gate`  y `Blade`


```php 
     Gate::define('admin', function (User $user) {
            return $user->username === 'Katniss29';
        });

        Blade::if('admin', function () {
            return request()->user()?->can('admin');
        });
```

```php 
                          <x-dropdown-item href="/admin/posts" :active="request()->is('admin/posts')">Dashboard</x-dropdown-item>
                        <x-dropdown-item href="/admin/posts/create" :active="request()->is('admin/posts/create')">New Post</x-dropdown-item>
                        @admin
                            <x-dropdown-item href="/admin/posts" :active="request()->is('admin/posts')">Dashboard</x-dropdown-item>
                            <x-dropdown-item href="/admin/posts/create" :active="request()->is('admin/posts/create')">New Post</x-dropdown-item>
                        @endadmin
```

```php 
    Route::middleware('can:admin')->group(function () {
    Route::resource('admin/posts', AdminPostController::class)->except('show');
    });
```
