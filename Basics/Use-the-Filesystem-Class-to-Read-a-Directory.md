## Use the Filesystem Class to Read a Directory 

- Para este video empezamos quitandole las etiquetas a los archivos que tenemos en la carpeta post.

###  **Crear una nueva clase:** 

- Para este punto creamos una nueva clase en la carpeta de `Models` que se encuentra en app llamada `Post`.
- Y la importamos en `web.php`

### **Se agrega el codigo que en un inicio estaba en `web. php`:**  

```php
<?php 

namespace App\Models;

class Post 
{
    public static function find($slug){
        
        if (!file_exists($path = resource_path("posts/{$slug}.html"))) {
            throw new ModelNotFoundException();
        }

        
        return cache()->remember("posts.{$slug}", 1200, fn() => file_get_contents($path)); 
        
    }
}

```

### **Se modifica el archivo `web.php`:** 

```php

Route::get('posts/{post}', function ($slug) {

    // Find a post by its slug and pass it to a view called "post"

    $post = Post::find($slug);

    return view('post', [
        'post' => $post

    ]);

    

})->where('post', '[A-z_\-]+');

```

- Esto le pasa el post seleccionado a la clase `Post`


### **Se modifica el archivo `posts.blade.php`: **

- En este paso se le agrega un foreach para que muestre los 3 posts

```php

<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>

    <?php foreach ($posts as $post) : ?> 

        <article>

            <?= $post; ?>

        </article>

    <?php endforeach; ?>
    
</body>

```


### **Se Crea una funcion en la clase `Post.php` llamada `all`:** 

- Esta funcion lo que permite es buscar todos los archivos en el directorio `resources/posts/` , lee el contenido de cada uno de los archivo y devuelve un array con el contenido de los archivos encontrados.

```php

<?php 

namespace App\Models;

use Illuminate\Database\Eloquent\ModelNotFoundException;
use Illuminate\Support\Facades\File;



class Post 
{

    public static function all(){

        $files = File::files(resource_path("posts/"));

        return array_map(fn($file) => $file ->getContents(), $files);
       

     
    }

    public static function find($slug){
        
        if (!file_exists($path = resource_path("posts/{$slug}.html"))) {
            throw new ModelNotFoundException();
        }

        
        return cache()->remember("posts.{$slug}", 1200, fn() => file_get_contents($path));

        
        
        
    }
}

```


### **Se modifican las rutas:** 

```php

Route::get('/', function () {
    return view('posts', [
        'posts' => Post::all()
    ]);
});

Route::get('posts/{post}', function ($slug) {
    // Find a post by its slug and pass it to a view called "post"
    return view('post', [
        'post' => Post::find($slug) // Aquí se eliminó el punto y coma incorrecto
    ]);
})->where('post', '[A-z_\-]+');

Auth::routes();

Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

```




























```php

<?php 

namespace App\Models;

use Illuminate\Database\Eloquent\ModelNotFoundException;
use Illuminate\Support\Facades\File;



class Post 
{

    public static function all(){

        $files = File::files(resource_path("posts/"));

        return array_map(fn($file) => $file ->getContents(), $files);
       

     
    }

    public static function find($slug){
        
        if (!file_exists($path = resource_path("posts/{$slug}.html"))) {
            throw new ModelNotFoundException();
        }

        
        return cache()->remember("posts.{$slug}", 1200, fn() => file_get_contents($path));

        
        
        
    }
}

```


