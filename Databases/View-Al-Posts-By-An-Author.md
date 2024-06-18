- [Volver a las rutas](/Readme.md)

## View All Posts By An Author

## Pasos para el video

### 1. Crear una nueva ruta en  `web.php` para ver la URL el username del creador del post

```php
   Route::get('authors/{author:username}', [CategoryController::class, 'authors']);
```


```php
   public function authors(User $author)
    {
        return view('posts', [
            'posts' => $author->posts
        ]);
    }
```

### 2. Modificar los archivos de  `post` y `posts:


```php
   <p>
         By <a href="/authors/{{ $post->author->username }}">{{ $post->author->name }}</a>in<a href="/categories/{{ $post->category->slug }}"> in {{ $post->category->name }}</a>
     </p>
```

### 3. Se crea una funcion en `Post`:


```php
  public function author(): BelongsTo
    {
        return $this->belongsTo(User::class, 'user_id');
    }
```

### 4. Se agrega un nuevo atributo en `createTable`:


```php
   public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('username')->unique();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }
```

- seguido de esto ejecutamos los comandos de migrate:fresh --seed que ya conocemos

