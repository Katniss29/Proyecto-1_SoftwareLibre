- [Volver a las rutas](/Readme.md)

## Route Wildcard Constraints

- Para este video solo realizamos ambios en `web.php` donde le agregamos una restriccion a la url de la siguiente manera.
  
```php

Route::get('posts/{post}', function ($slug) {
    
    $path =  _DIR_ . "/../resources/posts/{$slug}.html";

    if(! file_exists($path)) {
        
        //dd('file does not exists');

        //ddd('file does not exists');

        //abort(404);

        return redirect('/');

    }

    $post = file_get_contents($path);

    return view('post', [
        'post' => $post
        
    ]);
    
})->where('post', '[A-z_\-]+');

```

- Esta restriccion es para asegurar que el valor pasado por la URL para `post` solo tenga caracteres alfabeticos tanto mayusculas como minusculas, guines bajos y guiones medios.  