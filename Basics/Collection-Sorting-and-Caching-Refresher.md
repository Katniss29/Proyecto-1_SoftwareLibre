- [Volver a las rutas](/Readme.md)
  

## Collection Sorting and Caching Refresher

- Para este video vemos la forma de ordenar las publicaciones por orden de fechas.


```php

public static function all()
    {

        return collect(File::files(resource_path("posts")))
            ->map(fn($file) => YamlFrontMatter::parseFile($file))
            ->map(fn($document) => new Post(
                $document->title,
                $document->excerpt,
                $document->date,
                $document->body(), 
                $document->slug
        ))

        ->sortBy('date');

     
    }

```

- Le agregamos un ` ->sortBy('date');` para ordenar segun la fecha de la publicacion.

### **Ejecutamos el comando de `php artisan tinker`**

- El cual es una herramienta para interactuar directamente con la aplicacion Laravel desde la linea de comandos, esto facilita el desarrollo y la depuracion de la aplicacion web basadas en Laravel.


### **Ejecutamos el comando de `cache('posts.all')`**

- Muestra todas las publicaciones en consola. 

### **Ejecutamos el comando de `cache()->forget('posts.all')`**

- Esto nos devuelve un `true`

