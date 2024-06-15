## How a Route Loads a View 

Para este inicio del curso, le echamos un vistazo a los archivos que tenemos en el `proyecto lfts.isw811.xyz`.

En este proyecto podemos observar diferentes archivos y documentos. En este video, exploramos las carpetas de `routes` y `resources`.

### Exploración de Carpetas

- **Carpeta `resources`:** 
  - Exploramos el archivo `welcome.blade.php`, el cual contiene el HTML del sitio web.

- **Carpeta `routes`:** 
  - Exploramos el archivo `web.php`, encargado de manejar las rutas y mostrar las páginas HTML.

En `web.php`, realizamos diferentes pruebas para ver cómo se comporta el sitio web con distintas formas de mostrar la página de inicio.

## Ejemplos 

1. **Return `view('welcome')`**

   Para mostrar la página principal donde se encuentra todo el HTML:

   ```php
   Route::get('/', function () {
       return view('welcome');
   });

   Auth::routes();

   Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');
   ```

2. **Return `Hello Word`**
    
    En este tipo de Return observaremos una especia de h2 con la palabra `Hello Word` 

      ```php
   Route::get('/hello', function () {
    return "Hello Word";
    });

    Auth::routes();

    Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

    como podemos ver la url `/hello` es difetente, esto indica como puedemos modificar las rutas segun las necesitemo


3. **Return `['foo' => 'bar']`**
    
    En este tipo de Return vemos un ` foo bar `   JSON 

      ```php
      Route::get('/', function () {
    return ['foo' => 'bar'];
    });

    Auth::routes();

    Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

   

  

