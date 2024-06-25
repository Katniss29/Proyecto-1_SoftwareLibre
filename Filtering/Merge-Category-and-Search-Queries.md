- [Volver a las rutas](/Readme.md)

## Merge Category and Search Queries

## Para este codigo modificamos dos archivos nada mas `category-dropdown` y `_header`


### Para el archivo `category-dropdown` agregamos el siguiente codigo 


```php

    <x-dropdown-item 
        href="/?{{ http_build_query(request()->except('category', 'page')) }}"
        :active="request()->routeIs('home')">All
    </x-dropdown-item>

    href="/?category={{ $category->slug }}&{{ http_build_query(request()->except('category', 'page')) }}"
    
```

- El cual genera un elemento de un menu desplegable que crea un enlace que comumente se utiliza en filtros para permitir a los usuarios restablecer la seleccion de categorias y ver todos los elementos.


### Para el archivo de `_header` se agrega un formulario que se envia a la raiz del sitio  utilizando el metodo `GET`. Si la solicitud actual contiene un aprametro `category`, el formulario incluira un campo oculto que mantiene el te valor.


```php

     <form method="GET" action="/">
        @if (request('category'))
            <input type="hidden" name="category" value="{{ request('category') }}">
        @endif
    
```
