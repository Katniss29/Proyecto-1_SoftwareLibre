## Use Caching for Expensive Operations 

- Para este video utilizamos la cache para recordar el sitio web

### Ejemplo 

```php

Route::get('posts/{post}', function ($slug) {

    if (!file_exists($path = _DIR_ . "/../resources/posts/{$slug}.html")) {
        return redirect('/');
    }

    
    $post = cache()->remember("posts.{$slug}", 1200, fn() => file_get_contents($path));

    
    return view('post', ['post' => $post]);

})->where('post', '[A-z_\-]+');

```