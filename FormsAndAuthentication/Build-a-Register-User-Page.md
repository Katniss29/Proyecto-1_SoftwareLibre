## Build a Register User Page

## Para este video creamos el register para la pagina para esto realizamos los siguientes pasos.

### Creamos un archivo llamado `RegisterController` con el siguiente comando.

- `php artisan make:controller RegisterController`

### Agregamos el siguiente codigo al archivo 

```php
    <?php

    namespace App\Http\Controllers;

    use App\Models\User;

    class RegisterController extends Controller
    {
        public function create()
        {
            return view('register.create');
        }

        public function store()
        {
            $attributes = request()->validate([
                'name' => 'required|max:255',
                'username' => 'required|min:3|max:255',
                'email' => 'required|email|max:255',
                'password' => 'required|min:7|max:255',
            ]);

            User::create($attributes);

            return redirect('/');
        }
    }

```


- Este controller gestiona el registro de neusvos usuarios.

### Creamos el form para el register en un archivo nuevo llamado `create.blade.php`


### Modificamos el archivo de `User.php`


-  `protected $guarded = [];`
-  Esto indica que no hay atributos protegidos contra la asignacion en masa. Esto significa que puedes asignar cualquier atributo del modelo utilizando la asignacion en masa sin restricciones.
-  

### Modificamos las rutas para que funcionen correctamete 

```php
    Route::get('registers', [RegisterController::class, 'create'])->middleware('guest');
    Route::post('registers', [RegisterController::class, 'store'])->middleware('guest');
```