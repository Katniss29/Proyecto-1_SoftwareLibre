## Validate and Store Post Thumbnails 

## Para este video se creo un link para cargar las imagenes, se activa el modo public en  `filesystems `, se agrega el atributo para guardar como una ip en la base de datos llamada  `$table->string('thumbnail')->nullable(); ` se hace el migrate fresh, se agrega las rutas para cargar las imagenes asignadas en los diferentes componentes.

```php
     $attributes = request()->validate([

    'thumbnail' => 'required|image',

     $attributes['thumbnail'] = request()->file('thumbnail')->store('thumbnails');
```

```php
    'default' => env('FILESYSTEM_DRIVER', 'public'),
```

```php
   $table->string('thumbnail')->nullable();
```


```php
<article {{ $attributes->merge(['class' => 'transition-colors duration-300 hover:bg-gray-100 border border-black border-opacity-0 hover:border-opacity-5 rounded-xl']) }}>

<img src="{{ asset('storage/' . $post->thumbnail) }}" alt="Descripción de la imagen">
```


```php
              <h1 class="text-lg font-bold mb-4">
                Publish New Post
            </h1>

            <x-panel>
                <form method="POST" action="/admin/posts" enctype="multipart/form-data">
```


