- [Volver a las rutas](/Readme.md)

## Route Model Binfing

## Paso para el video

### 1. **Modificamos el archivo `web`:**

- Para colocar la url mas completa modificamos el archivo con el siguiente codigo.

```php
    Route::get('posts/{post:slug}', function (Post $post) {

        return view('post', [
            'post' =>  $post
        ]);
    });

    Auth::routes();

    Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

```

### 2. **Modificamos el model de la bases de datos de `posts`**

- Para esto agregamos el siguiente codigo.

```php
  public function up()
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->string('slug')->unique();
            $table->string('title');
            $table->text('excerpt');
            $table->text('body');
            $table->timestamps();
            $table->timestamp('publisher_at')->nullable();
            
        });
    }

```

### 3. **Realizamos el siguiente comando**

- `php artisan migrate:fresh`

### 4. ** Hacemos un nuevo inserta para agregar los atributos `slug`**


```mysql
    INSERT INTO posts (id, slug, title, excerpt, body, created_at, updated_at, publisher_at) VALUES
    (2, 'my-second-post', 'My Second Post', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur assumenda fugit expedita cumque eius nesciunt. Nulla ipsa eaque distinctio? Sunt aut quibusdam illum ad illo doloribus accusamus dolorem pariatur repellat.', '<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Pariatur assumenda fugit expedita cumque eius nesciunt. Nulla ipsa eaque distinctio? Sunt aut quibusdam illum ad illo doloribus accusamus dolorem pariatur repellat.</p>', '2024-06-17 18:04:30', '2024-06-17 21:45:54', NULL),
    (3, 'my-thierd-post', 'My Third Post', 'Excerpt of post', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam quisquam nisi quia porro error nobis tenetur? Ducimus reiciendis consectetur error nisi illum placeat voluptas aut itaque! Deleniti, quisquam ab? Ipsa?', '2024-06-17 22:44:27', '2024-06-17 22:44:27', NULL),
    (4, 'my-fourth-post', 'My Fourth Post', 'excerpt of post', 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam quisquam nisi quia porro error nobis tenetur? Ducimus reiciendis consectetur error nisi illum placeat voluptas aut itaque! Deleniti, quisquam ab? Ipsa?', '2024-06-17 22:54:49', '2024-06-17 22:54:49', NULL);
```


