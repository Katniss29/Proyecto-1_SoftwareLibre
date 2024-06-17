## Layouts Two Ways

### **Creacion de una nueva carpeta llamada `components` y un archivo dentro de ella llamado `layout.blade.php`**

- Este archivo se encarga de tener una plantilla reutilizable que puede incluir otras vistas.


```php
<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
   
    {{ $slot }}

</body>

```

### **Modificamos el archivo `posts` para utilizar `layout` de la mejor mandera**

- Para esto utilizamos la vista que utiliza el componente `layout`


```php

    <x-layout>

        @foreach ($posts as $post)
            
            <article>
                <h1>
                    <a href="/posts/{{ $post->slug }}">
                        {{ $post->title }}
                    </a>
                </h1>

                <div>
                    {{ $post->excerpt }}
                </div>
            </article>
        @endforeach

    </x-layout>

```


### **Finalmente modificamos el archivo `post`**

- Para la modificacion utilizamos `@extends`: Que nos indica que esta vista hereda de una plantilla llamada `layout`.

- Tambien se utiliza `@section` Que define una seccion de contenido llamda `content` que se inserta en la ubicacion correspondiente de `@yield('content')` en el archivo `layout.blade.php`

```php

    @extends('layout')

    @section ('content')
        <article>

        <h1> {{ $post->title}}</h1>

        <div>
            {!! $post->body !!}
        </div>


        </article>

        <a href="/">Go Back</a>
    @endsection
```