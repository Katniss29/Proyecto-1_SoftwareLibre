- [Volver a las rutas](/Readme.md)

## Laravel Breeze Quick Peek


### Para este video em,empezamos modificando el archivo `SeccionController`

```php
   if (! auth()->attempt($attributes)) {
            throw ValidationException::withMessages([
                'email' => 'Your provided credentials could not be verified.'
            ]);
        }

        session()->regenerate();

        return redirect('/')->with('success', 'Welcome Back!');
    }
```

- Esto nos permite mejorar la autenticacion de usuarios de manera segura y para proporcionar retroalimentacion clara al usuario sobreel exito o fracaso de la operacion de autenticacion.


### Luego de esto creamos un segundo proyecto larave llamado `Demo`.

- En este proyecto vimos la manera mas facil de como hacer los pasos de login y register de una manera mas facil utilizando un archivo `databases.sqlite` para almacenar a los usuarios.

-Al final del video se borra el proyecto