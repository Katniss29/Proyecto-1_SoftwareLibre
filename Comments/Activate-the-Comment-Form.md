## Activate the Comment Form 

## Pasos para realizar el video

### 1 - Para este video creamos un nueov controller para permitir a los usuarios autenticados añadir comentarios a los posts.

```php 
    <?php

namespace App\Http\Controllers;

use App\Models\Post;
use Illuminate\Http\Request;

class PostCommentsController extends Controller
{
    public function store(Post $post)
    {
        request()->validate([
            'body' => 'required'
        ]);

        $post->comments()->create([
            'user_id' => request()->user()->id,
            'body' => request('body')
        ]);

        return back();
    }
}
```

### 2 - Agragamos  `Model::unguard(); ` al archivo  `AppServiceProvider `

- Esto para desactivar temporalmente la protección contra asignación masiva, facilitando operaciones como el seeding de base de datos.


### 3 - Se le agragan unas mejoras a  `show.blade.php ` 

```php
     <x-panel>
                <form method="POST" action="/posts/{{ $post->slug}}/comments"> 
```

 - Agregamos una ruta para los posts con el slug de cada posts



 ```php
    <textarea 
        name="body"  
        class="w-full text-sm focus:outline-none focus:ring" 
        rows="5" 
        placeholder="Quick, thing of something to say !"></textarea>            
 ```

 - Para escribir el comentario a publicar}


 ### 4 - Agregamos las rutas necesarias para el buen funcionamiento

 ```php
    Route::post('posts/{post:slug}/comments', [PostCommentsController::class, 'store']);

 ```

 