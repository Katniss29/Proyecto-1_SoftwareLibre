## The Absolute Basics

- Para este video observamos las diferencias entre `migrate:fresh `, `migrate:rollback`, `migrate`

1 . **Migrate**

- Este comando ejecuta todas las migraciones pendientes queaun no se han ejecutado en la base de datos.


2 . **Migrate:fresh**

- Este comando elimina todas las tablas de la base de datos y luego ejecuta todas las migraciones desde cero. Es util cuando se quiere restablecer completamente la estructura de la base de datos. `Migrate:fresh es mas drastico que migrate`

3 . **Migrate:rollback**

- Deshace la ultima migracion que se haya aplicado  a la base de datos.


- Por otro lado en el video tambien hacemos algunos cambios en la carpeta de `migrations` en la carpeta `create-users-table.php`

- Los cambios fueron los siguiente :

1 . Eliminar el atributo `timesstamp`

2 . Ejecutamos los siguientes comandos 

    - `php artisan migrate:rollback`
    - `php artisan migrate`
    - `php artisan migrate`
  
3 . Despues de esto creamos un `user` en TablaPlus con la interfaz y despues con un query