## Automatic Password Hashing With Mutators

### Para este video agragamos una funcion apra convertir el `Password` en una cadena encriptada


```php

   public function setPasswordAttribute($password)
    {
        $this->attributes['password'] = bcrypt($password);
    }

```
 