- [Volver a las rutas](/Readme.md)

## Advanced Eloquent Query Constraints

## Para este video se modifican varios archivos

### Eliminamos show de CategoryController

### Agregamos al controlador de `PostController` el metodo para manejar solicitudes HTTP quebuscan mostrar la lista de posts filtrados segun las categorias y lo queel usuario busque

```php
     
    $filters = [
            'search' => $request->input('search'),
            'category' => $request->input('category'),
        ];

        // Consultar los posts filtrados
        $posts = Post::latest()->filter($filters)->get();

        // Obtener todas las categorías
        $categories = Category::all();

        // Obtener la categoría actualmente seleccionada
        $currentCategory = null;
        if ($request->has('category')) {
            $currentCategory = Category::firstWhere('slug', $request->category);
        }

        // Retornar la vista con los posts, categorías y categoría actual
        return view('posts', compact('posts', 'categories', 'currentCategory'));
```

### Aregamos un filtro que devulve todos los posts que estan asociados a la categoria que se busque

```php

         $query->when($filters['category'] ?? false, function ($query, $category) {
            $query->whereHas('category', function ($query) use ($category) {
                $query->where('slug', $category);
            });
        });
    
```


###  Cambiamos el `href` de `_post-header`

 `href="/?category={{ $category->slug }}"`


 ### Agregamos la nueva ruta a `web`

```php

    Route::get('categories/{category}', [PostController::class, 'index'])->name('categories.posts');
    
```
