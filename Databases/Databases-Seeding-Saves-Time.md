## Database Seeding Saves Time

## Pasos para este video.


### 1. **Modificamos la migracion de  `post`.**

```php
   public function up()
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->foreignId('user_id');
            $table->foreignId('category_id');
            $table->string('slug')->unique();
            $table->string('title');
            $table->text('excerpt');
            $table->text('body');
            $table->timestamps();
            $table->timestamp('publisher_at')->nullable();
            
        });
    }

```

- Se le agrega el atributo de user_id


### 2. **Se ejecuta el siguiente comando  `php artisan migrate:fresh`.**

- Para restablecer la base de datos.


### 3. **Nos dirigimos a la carpeta  `seeders` y al archivo  `DatabaseSeeder` y se agrega el siguiente codigo**

```php

    public function run()
    {
        User::truncate();
        Category::truncate();
        Post::truncate();




        $user = User::factory()->create();

        $family = Category::create([
            'name' => 'Family',
            'slug' => 'family' 
        ]);

        $personal = Category::create([
            'name' => 'Personal',
            'slug' => 'personal' 
        ]);

        $work = Category::create([
            'name' => 'Work',
            'slug' => 'work' 
        ]);


        Post::create([
            'user_id' =>  $user->id,
            'category_id' => $family->id,
            'title' => 'My Family Post',
            'slug' => 'my-first-post',
            'excerpt' => ' <p> Lorem ipsum dolar sit amet. </p>',
            'body' => ' <p> Lorem, ipsum dolor sit amet consectetur adipisicing elit. Animi tempore earum id! Repellendus, laudantium itaque. Corrupti, vel similique. Expedita ratione voluptatibus id repudiandae natus ab inventore cupiditate iusto maxime eveniet.</p>'

        ]);

        
        Post::create([
            'user_id' =>  $user->id,
            'category_id' => $work->id,
            'title' => 'My Work Post',
            'slug' => 'my-work-post',
            'excerpt' => 'Lorem ipsum dolar sit amet.',
            'body' => 'Lorem, ipsum dolor sit amet consectetur adipisicing elit. Animi tempore earum id! Repellendus, laudantium itaque. Corrupti, vel similique. Expedita ratione voluptatibus id repudiandae natus ab inventore cupiditate iusto maxime eveniet.'

        ]);
    }
 
```


- Este codigo nos evita repetir usuarios, post, o categorias, ademas nos crea las categorias deseadas y dos post con el id user y con la categoria que deseemos

- Para esto ejecutamos el comando php artisan migrate:fresh --seed`


### 4. **Modificamos el codigo de  `post`**

```php
   <x-layout>

    <article>
        <h1>{!! $post->title !!}</h1>

        <p>

            By <a href="#">{{ $post->user->name }}</a> in <a href="/categories/{{ $post->category->slug }}">{{ $post->category->name }}</a>
        </p>

        <div>
            {!! $post->body !!}
        </div>
    </article>

    <a href="/">Go Back</a>
</x-layout>

```


