## Failed Validation and Old Input Data


## Para este video se agragan validaciones a los input y se agrega un validacion de que no exita ese usuario con ese correo registrado 

- `value="{{ old('name') }}"` 
- Se le agrag esta propidad a todos los input menos al `password` esto para validar que en la base de datos no exita 

```php
    @error('username')
        <p class="text-red-500 text-xs mt-1">{{ $message }}</p>
    @enderror

```


- Y este para los errores a la hora de ingrasar datos, se le agraga a todos los inputs