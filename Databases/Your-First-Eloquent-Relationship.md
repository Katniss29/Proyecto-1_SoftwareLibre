## Your First Eloquent Relationship 

## Paso para este video

### 1. **Creacion de una nueva tabla:**

- `php artisan make:migration create_categories_table` 

### 2. **Ejecutar el siguiente comando para crear el model:**

- `php artisan make:model Category -m `


### 3. **Agregamos nuevos atributos a las tablas de `posts` y `categories`:**


```bash

    public function up()
        {
            Schema::create('posts', function (Blueprint $table) {
                $table->id();
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

```php
 public function up()
    {
        Schema::create('categories', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('slug');
            $table->timestamps();
        });
    }
```
### 4. **Insertamos 3 `coregories` diferentes:**



```bash
    use App\Models\Category;
    > $c = new Category;
    = App\Models\Category {#4813}

    > $c->name = 'Personal';
    = "Personal"

    > $c->slug = 'personal';
    = "personal"

    > $c->save();
    = true

    > $c = new Category;
    = App\Models\Category {#4826}

    > $c->name = 'Word';
    = "Word"

    > $c->name = 'Work';
    = "Work"

    > $c->slug = 'work';
    = "work"

    > $c->save();
    = true

    > $c = new Category;
    = App\Models\Category {#5586}

    > $c->name = 'Hobbies';
    = "Hobbies"

    > $c->slug = 'hobbies';
    = "hobbies"

    > $c->save();
    = true
   
```





### 5. **Insertamos 3 `post` con diferentes `categories`:**

- De la siguiente manera


```bash
    
    $post->title = 'My First Post';
    = "My First Post"

    > $post->excerpt = 'Excerpt for my post';
    = "Excerpt for my post"

    > $post->body = 'Lorem ipsum, dolor sit amet consectetur adipisicing elit. Laudantium inventore numquam tempore sed. Exercitationem quis omnis ipsa! Vel doloribus, vero perspiciatis veniam magni adipisci nulla ex
    unde cum nobis molestias!';
    = "Lorem ipsum, dolor sit amet consectetur adipisicing elit. Laudantium inventore numquam tempore sed. Exercitationem quis omnis ipsa! Vel doloribus, vero perspiciatis veniam magni adipisci nulla ex unde cum nobis molestias!"

    > $post->slug = 'my-family-post';
    = "my-family-post"

    > $post->category_id = 1;
    = 1

    > $post->save();
    = true
`
```



### 6. **Se realizo un quey :**

-  `select * from posts where category_id = 3`
  

### 7. **Se crea una funcion para la clase Post para mostrar los datos de `categories` :**


```bash
    public function category()
    {
        return $this->belongsTo(category::class);
    }

```

### 8. **Se agrega la categoria a los archivos de `post` y `posts` :**

  
```bash
    <x-layout>

    @foreach ($posts as $post)
        
        <article>
            <h1>
                <a href="/posts/{{ $post->slug }}">
                    {!! $post->title !!}
                </a>
            </h1>

            <p>
                <a href="#">{{ $post->category->name}}</a>
            </p>

            <div>
                {{ $post->excerpt }}
            </div>
        </article>
    @endforeach

</x-layout>
   
```


```bash
    <x-layout>


    <article>
        <h1> {!! $post->title !!}</h1>

        <p>
                <a href="#">{{ $post->category->name}}</a>
            </p>


        
        <div>
            {!! $post->body !!}
        </div>
    </article>


    <a href="/">Go Back</a>
</x-layout>
   
```
