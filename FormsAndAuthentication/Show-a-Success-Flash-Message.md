## Show a Success Flash Message

### Para este video agragamos un mensaje de registro exitoso

- ` return redirect('/')->with('success', 'Your account has been created.');`


- Agregamos la renderizacion con el mensaje correcto esto en el archivo de `RegisterController`


### Creamos un nuevo componente llamado `flash`

```php
    @if (session()->has('success'))
    <div x-data="{ show: true }"
         x-init="setTimeout(() => show = false, 4000)"
         x-show="show"
         class="fixed bg-blue-500 text-white py-2 px-4 rounded-xl bottom-3 right-3 text-sm"
    >
        <p>{{ session('success') }}</p>
    </div>
@endif
```


- Este codigo crea un mensaje de exito que se muestra de manera discreta en la esquina inferior derecha de la pantalla.


### Finalmente se agrega el componente al archivo `layout.blade.php`


- `<x-flash />`