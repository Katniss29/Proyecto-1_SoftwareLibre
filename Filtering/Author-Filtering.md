- [Volver a las rutas](/Readme.md)

## Author Filtering 

 - Para este video se reliza la funcionalidad de busqueda por `author`
  
### Agregar una consulta para filtrar datos en funcion de parametros de entrada en una solicitud `HTTP`

```php

    $query->when($filters['author'] ?? false, fn($query, $author) =>
            $query->whereHas('author', fn ($query) =>
                $query->where('username', $author)
            )
        );
    
```

### Agregar el enlace para esa consulta, tanto al archivo de `post-cart` como al de `post-featured-card`

```php

     <h5 class="font-bold">
        <a href="/?author={{ $post->author->username }}">{{ $post->author->name }}</a>
    </h5>
    
```



