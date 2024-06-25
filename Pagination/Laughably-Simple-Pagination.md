- [Volver a las rutas](/Readme.md)

## Laughably Simple Pagination

## Para este video logramos hacerle el `pagination` al sitio web.


### Agragamos el siguiente codigo

```php

    'posts' => Post::latest()->filter(
                        request(['search', 'category', 'author'])
                    )->paginate(6)->withQueryString()
        ]);

```


- Nos permite construir y ejecutar una consulta para obtener las publicaciones mas recientes desde la base de datos, filtradas segun los parametros de busqueda, categoria y author, proporcionandos en la solicitud `HTTP`.
- Luego se paginan los resultados para mostrar publicaciones por pagina.


###  Agragamso ` {{ $posts->links() }}` a el archivo `index`

- Esto nos permite mostrar enlaces de paginacion para una coleccion de resultados paginados.

### Creamos con el comando `php artisan vendor:publish` y selecionamos la opcion de `laravel-pagination`

- Esto nos permite publicar recursos de un paquete de proveedor en la aplicacion. Permitiendo personalizar y modificar los archivos de configuracion, vistas y otros recursos proporcionados por un paquete de terceros.
