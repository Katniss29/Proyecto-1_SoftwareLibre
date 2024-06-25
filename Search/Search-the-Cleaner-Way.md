- [Volver a las rutas](/Readme.md)

## Search (The Cleaner Way)

## Para este video se estructuro el codigo de una manera diferente

### Se crea  el controller `PostController`

```php

   class PostController extends Controller
    {
        public function index()
        {
            return view('posts', [
                'posts' => Post::latest()->filter(request(['search']))->get(),
                'categories' => Category::all()
            ]);
        }

        public function show(Post $post)
        {
            return view('post', [
                'post' => $post
         ]);
        }
    }

```

- Este Controller se encarga de manejar la logica de mostrar listas de posts y posts individuales.

### Se modifica el archivo `Post.php`


```php

    public function scopeFilter($query, array $filters)
    {
        $query->when($filters['search'] ?? false, fn($query, $search) =>
            $query
                ->where('title', 'like', '%' . $search . '%')
                ->orWhere('body', 'like', '%' . $search . '%'));
    }

```

- Se encarga de manejar el query de la base de datos para mostrar las busqueda


### Se modifica el archivo `_post-header`

```php
     <input type="text"
        name="search"
        placeholder="Find something"
        class="bg-transparent placeholder-black font-semibold text-sm"
        value="{{ request('search') }}"
    >
    
```

- Se modifica el input de busqueda y enviar terminos de busqueda, yutilizando Laravel para prellenar el campo con el termino actual en caso de que la pagina se recargue o se navegue con un parametro de busqueda en la URL.


### Se modifica el archivo `web.php`

```php
    Route::get('/', [PostController::class, 'index'])->name('home');
    Route::get('posts/{post:slug}', [PostController::class, 'show']);
    
```

- Se modifica las rutas que manejan la visualizaciones de una lista de posts y la visualizacion de un posts en especifico