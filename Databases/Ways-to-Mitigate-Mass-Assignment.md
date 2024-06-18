- [Volver a las rutas](/Readme.md)

## Ways to Mitigate Mass Assignment Vulnerabilities

## Pasos del video

### 1. **Crear otro post**

```bash
    > use App\Models\Post;
    > $post = new Post;
    = App\Models\Post {#4815}

    > $post->title = 'My Third Post';
    = "My Third Post"

    > $post->excerpt = 'Excerpt of post';
    = "Excerpt of post"

    > $post->body = 'Lorem ipsum dolor sit amet consectetur adipisicing elindis consectetur error nisi illum placeat voluptas aut itaque! Deleniti
    = "Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam ur error nisi illum placeat voluptas aut itaque! Deleniti, quisquam ab?

    > $post->save();
    = true
```

### 2. **Creamos un 4 post de manera conjunta o masiva**


- Esto quiere decir que en un solo comando re agregan los 3 atributos `title`, `excerpt`,`body`.

```bash
    `Post::create(['title' => 'My Fourth Post', 'excerpt' => 'excerpt of post', 'body' => 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam quisquam nisi quia porro error nobis tenetur? Ducimus reiciendis consectetur error nisi illum placeat voluptas aut itaque! Deleniti, quisquam ab? Ipsa?']);`

```

- Le realizamos un cambio al archivo `Post` para cargar el comando sin nigun problema.

```php
    <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Post extends Model
    {
        use HasFactory;

        protected $fillable = ['title', 'excerpt', 'body'];
    }
```

### 3. **Al final le cambiamos el `excerpt` a el primer post**

- Con el siguiente comando 

    - `$post->update(['excerpt' => 'Changed'])`