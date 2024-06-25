- [Volver a las rutas](/Readme.md)

## Login and Logout


### Para este video creamos ls ruta de login y  creamos el controller de login para gestionar la autenticacion de sesiones de usuario.

```php
    <?php

    namespace App\Http\Controllers;

    use Illuminate\Validation\ValidationException;

    class SessionsController extends Controller
    {
        public function create()
        {
            return view('sessions.create');
        }

        public function store()
        {
            $attributes = request()->validate([
                'email' => 'required|email',
                'password' => 'required'
            ]);

            if (auth()->attempt($attributes)) {
                session()->regenerate();

                return redirect('/')->with('success', 'Welcome Back!');
            }

            throw ValidationException::withMessages([
                'email' => 'Your provided credentials could not be verified.'
            ]);
        }

        public function destroy()
        {
            auth()->logout();

            return redirect('/')->with('success', 'Goodbye!');
        }
    }

```

- `Route::post('logout', [SessionsController::class, 'destroy'])->middleware('auth');`

### Cambiamos la ruta en el archivo de `RouteServiceProvider` para que renderice a la pagina raiz

- ` public const HOME = '/';`

### Agregamos los enlaces a la pagina principal de registro y login 


```php

   <div class="mt-8 md:mt-0 flex items-center">
                @auth
                    <span class="text-xs font-bold uppercase">Welcome, {{ auth()->user()->name }}!</span>

                    <form method="POST" action="/logout" class="text-xs font-semibold text-blue-500 ml-6">
                        @csrf

                        <button type="submit">Log Out</button>
                    </form>
                @else
                    <a href="/registers" class="text-xs font-bold uppercase">Register</a>
                    <a href="/loginn" class="ml-6 text-xs font-bold uppercase">Log In</a>
                @endauth

```