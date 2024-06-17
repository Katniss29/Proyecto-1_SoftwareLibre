## Make a Post Model and Migration 

- Para este video empezamos borrando el archivo de `Post`

- Luego creamos un archivo `create-posts-table` desde consola

```bash 

    vagrant@webserver:~/sites/lfts.isw811.xyz$ php artisan make:migration create-posts-table
    Created Migration: 2024_06_17_173208_create-posts-table
```

- Modificamos este archivo con base a los atributos que queremos que tenga la base de datos.

```php
    <?php

    use Illuminate\Database\Migrations\Migration;
    use Illuminate\Database\Schema\Blueprint;
    use Illuminate\Support\Facades\Schema;

    class CreatePostsTable extends Migration
    {
        /**
         * Run the migrations.
         *
         * @return void
         */
        public function up()
        {
            Schema::create('posts', function (Blueprint $table) {
                $table->id();
                $table->string('title');
                $table->text('excerpt');
                $table->text('body');
                $table->timestamps();
                $table->timestamp('publisher_at')->nullable();
                
            });
        }

        /**
         * Reverse the migrations.
         *
         * @return void
         */
        public function down()
        {
          //
        }
    }
```

- Realizamos un `php artisan migrate`

- Ejecutamos el comando `php artisan make:model Post` para crear un modelo Eloquent para una tabla de bases de datos.

- Seguido de esto al igual que los users, creamos los posts que necesitemos.

-`php artison serve` para crear el archivo `Post`


- Le hacemos cambios a los posts para pasarle el `id` y no el `slug` al igual que a al archivo `web`

```php
    Route::get('/', function () {
    
        return view('posts', [
            'posts' => Post::all()
        ]); 
    });


    Route::get('posts/{post}', function ($id) {

        return view('post', [
            'post' =>  Post::findOrFail($id)
        ]);
    });

    Auth::routes();

    Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

```


```php

<x-layout>

    @foreach ($posts as $post)
        
        <article>
            <h1>
                <a href="/posts/{{ $post->id }}">
                    {{ $post->title }}
                </a>
            </h1>

            <div>
                {{ $post->excerpt }}
            </div>
        </article>
    @endforeach

</x-layout>

```