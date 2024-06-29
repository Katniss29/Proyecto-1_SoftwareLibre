## Make the Comments Section Dynamic 

### Para este video creamos los comentario directamente, y los entrelazamos a diferentes usuarios y  a diferentes post  para esto 

```php

    public function post()
    {
        return $this->belongsTo(Post::class);
    }

    public function author()
    {
        return $this->belongsTo(User::class, 'user_id');
    }


```

- La función `post` define una relación de pertenencia entre el modulo actual y el modelo `Post`.

- `author` define una relación perteneciente entre el modelo actual y el modelo `User`

### Definimos y utilizamos una relacion de `Tiene muchos`, facilitando la gestion de datos relacionados.

```php

      public function comments()
    {
        return $this->hasMany(Comment::class);
    }

```

### Agregamos el modelo para crear directamente los comentarios 

```php

    <?php

namespace Database\Factories;

use App\Models\Comment;
use App\Models\Post;
use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;

class CommentFactory extends Factory
{
    /**
     * The name of the factory's corresponding model.
     *
     * @var string
     */
    protected $model = Comment::class;

    /**
     * Define the model's default state.
     *
     * @return array
     */
    public function definition()
    {
        return [
            'post_id' => Post::factory(),
            'user_id' => User::factory(),
            'body' => $this->faker->paragraph()
        ];
    }
}

```

### Agragamos los atributos adecuados al componente de `post-comment.blade.php`

```php
    @props(['comment'])

     <img src="https://i.pravatar.cc/60?u={{ $comment->id }}" alt="" width="60" height="60" class="rounded-xl">

     <h3 class="font-bold">{{ $comment->author->username }}</h3>

      <time>{{ $comment->created_at }}</time>

    {{ $comment->body }}

```

### Se agrega el componente en un foreach para recorrer los comentarios 

```php

     @foreach ($post->comments as $comment)
                        <x-post-comment :comment="$comment" />
    @endforeach

```