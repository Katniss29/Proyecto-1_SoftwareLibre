- [Volver a las rutas](/Readme.md)


## Fix a Confusing Eloquent Query Bug

### Para este video solo trabajamos con el archivo `Post` 


```php

 $query->where(fn($query) =>
                $query->where('title', 'like', '%' . $search . '%')
                    ->orWhere('body', 'like', '%' . $search . '%')
            )
        );
    
```

- Al igual como lo venismo trabajando en otros video esto lo que nos ayuda es a construir una consulta condicional que filtra resultados basados en un filtro de busqueda.