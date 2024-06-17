## Enloquent Updates and HTML Escaping

## Pasos del video

### 1. **Utilizar el comando `php artisan tinker`:**



### 2. **Utilizar el comando `$post = App\Models\Post::first():` para ver el primer post de la base de datos:**

### 3. **Se modifica el `body` con el siguiente comando:**

- `$post->body = '<p>' . $post->body . '</p>';`

- Tanto del primer post como del segundo.

- Se guarda cada cambio con el siguiente comando.

- `$post->save();`

### 4. **Se modifica el title de el primer post con el siguiente comando.**

- `$post->title = 'My Post <script>alert("hello")</script>';` 
  
- Se guarda cada cambio con el siguiente comando.

- `$post->save();`

### 5. **Se modifica el `title` de `post` y `posts` para poder mostrarlo correctamente.**

```php
    <x-layout>


        <article>
            <h1> {!! $post->title !!}</h1>

            
            <div>
                {!! $post->body !!}
            </div>
        </article>


        <a href="/">Go Back</a>
    </x-layout>
```

```php
    <x-layout>

        @foreach ($posts as $post)
            
            <article>
                <h1>
                    <a href="/posts/{{ $post->id }}">
                        {!! $post->title !!}
                    </a>
                </h1>

                <div>
                    {{ $post->excerpt }}
                </div>
            </article>
        @endforeach

    </x-layout>

```

### 6. **Luego al `title` del primer post le agragamos un alert.**

   - `$post->title = 'My Post <script>alert("hello")</script>';`
  
- Se guarda cada cambio con el siguiente comando.

  - `$post->save();`