- [Volver a las rutas](/Readme.md)

## Clockwork, and N + 1 Problem

## Pasos

### 1. **Para este video empezamos modificando la ruta principal para que observar lso movimientos de la base de datos en el archivo `laravel.log`

### 2. **Luego instalamos clockWork con el comando `composer require itsgoingd/clockwork`**


### 3. **Luego agregamos la extencion a chrome**


### 4. **Luego realizamos cambios en el archivo `.env` y `clockwork.php` ya que si no sale vacia la extencion**

- `.env`

```php
   'enable' => env('CLOCKWORK_ENABLE', true), 
```

- `clockwork.php`

```php

    APP_NAME=Laravel
    APP_ENV=local
    APP_KEY=base64:SJlJ2OhhUulwtQMF0gDOYuIqJVvpkZFhof6+dhFPlZo=
    APP_DEBUG=true
    CLOCKWORK_ENABLE=true
    APP_URL=http://localhost
```

### 5. **Ejecutamos los siguientes comandos**

- `php artisan config:cache`
  
-  `php artisan config:clear`
-  
- Para limpiar la cache y que no hayan errores

### 6. **Modificar el archivo `web.php` para ver el funcionamiento en clockwork**

```php
   Route::get('/', function () {

  
    return view('posts', [
        'posts' => Post::with('category')->get()
    ]); 
});
```


### 7. **Ver desde chrome con la herramienta de clockwork las solicitudes de la base de datos**
