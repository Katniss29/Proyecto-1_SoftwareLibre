## Eloquent and the Active Record Pattern

1 .  El primer paso de este video es volver el archivo `create-users-table` a su codigo original.


2 . Seguido ejecutamos el siguiente comando `php artisan migrate:fresh`

3 . Despues de esto aprendemos a crear `users` desde `tinker`

### Ejemplo

- Como se crea el user desde tinker

```bash

    > $user = new App\Models\User;
    = App\Models\User {#4815}

    > $user = new User;
    [!] Aliasing 'User' to 'App\Models\User' for this Tinker session.
    = App\Models\User {#4813}

    > $user->name = 'EmilyArce';
    = "EmilyArce"

    > $user->email = 'arceemi29@gmail.com';
    = "arceemi29@gmail.com"

    > $user->password = bcrypt('!passwprd');
    = "$2y$10$W7aQuvC6V8k/iSx0bCZwjOIuuLpRKBdgt81cmfFN.Ug.bMhxO2lZO"

    > $user->save();
    = true


```

- Como ver el `user` recien creado 

 ```bash
    > $user
    = App\Models\User {#4813
        name: "EmilyArce",
        email: "arceemi29@gmail.com",
        #password: "$2y$10$W7aQuvC6V8k/iSx0bCZwjOIuuLpRKBdgt81cmfFN.Ug.bMhxO2lZO",
        updated_at: "2024-06-17 16:34:03",
        created_at: "2024-06-17 16:34:03",
        id: 1,
      }

```

- Como renombrar el `user` recien creado
 
 ```bash 
    > $user->name = 'JohnDoe';
    = "JohnDoe"

    > $user->save();
    = true

    > User::find(1);
    = App\Models\User {#4830
        id: 1,
        name: "JohnDoe",
        email: "arceemi29@gmail.com",
        email_verified_at: null,
        #password: "$2y$10$W7aQuvC6V8k/iSx0bCZwjOIuuLpRKBdgt81cmfFN.Ug.bMhxO2lZO",
        #remember_token: null,
        created_at: "2024-06-17 16:34:03",
        updated_at: "2024-06-17 16:48:41",
      }

```

- Como ver los `users` creados

```php
    > $users = User::all();
    = Illuminate\Database\Eloquent\Collection {#4830
        all: [
        App\Models\User {#5804
            id: 1,
            name: "JohnDoe",
            email: "arceemi29@gmail.com",
            email_verified_at: null,
            #password: "$2y$10$W7aQuvC6V8k/iSx0bCZwjOIuuLpRKBdgt81cmfFN.Ug.bMhxO2lZO",
            #remember_token: null,
            created_at: "2024-06-17 16:34:03",
            updated_at: "2024-06-17 16:48:41",
        },
        App\Models\User {#5817
            id: 2,
            name: "Sally",
            email: "sally@gmail.com",
            email_verified_at: null,
            #password: "$2y$10$G4pG9.1oyjbz0YqKr1rERu4sZNSSeGPgEhw1L9jdJQUoRQUxFuoRu",
            #remember_token: null,
            created_at: "2024-06-17 16:51:46",
            updated_at: "2024-06-17 16:51:46",
       },
        ],
      }

```

- Ver solo los nombres de los `user`

```php
    > $users->pluck('name');
    = Illuminate\Support\Collection {#5811
        all: [
        "JohnDoe",
        "Sally",
        ],
      }

```