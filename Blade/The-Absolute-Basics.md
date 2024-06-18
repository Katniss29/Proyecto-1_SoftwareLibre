- [Volver a las rutas](/Readme.md)
- 
## The Absolute Basics

- Para este video exploramos las carpetas de `view` y `logs`

### **Modificamos el archivo `post`:**

```php
<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
    <article>

        <h1> {{ $post->title}}</h1>

        <div>
            {!! $post->body !!}
        </div>
      

    </article>
    
    <a href="/">Go Back</a>
</body>

```

- Se realizan cambios a la hora de mostrar el titulo y el cuerpo de la publicacion,para esto la sintaxis `{!! $post->body !!}` marca como texto importante.

### **Se modifica el archivo `posts`**

- Con el mismo fin de remarcar lo necesario.

```php

<!doctype html> 

<title>My Blog</title>

<link rel="stylesheet" href="/app.css">


<body>
    @foreach ($posts as $post)
        @dd($loop)
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
    
</body>
```

### **Nota**

- Cuando trabajamos con Blade, la directiva `@foreach` se utiliza para iterar sobre una coleccion de elementos y renderizar contenido HTML
