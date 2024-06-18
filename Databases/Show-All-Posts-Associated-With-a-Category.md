- [Volver a las rutas](/Readme.md)

## Show All Post Associated With A Category

## Pasos para el video 


### 1. **Crear una ruta para categories:**


```php
   Route::get('categories/{category}', function (Category $category) {

    return view('posts', [
        'posts' => $category->posts
    ]);
});
```


### 2. **Modificar los Archivos `Post`, `Category`, `posts` y `post` para el buen funcionamiento de la ruta:**


```php
   <x-layout>

    @foreach ($posts as $post)
        
        <article>
            <h1>
                <a href="/posts/{{ $post->slug }}">
                    {!! $post->title !!}
                </a>
            </h1>

            <p>
                <a href="/categories/{{ $post->category->id }}">{{ $post->category->name}}</a>
            </p>

            <div>
                {!! $post->excerpt !!}
            </div>
        </article>
    @endforeach

</x-layout>
   
```

```php

   <x-layout>


    <article>
        <h1> {!! $post->title !!}</h1>

        <p>
            <a href="/categories/{{ $post->category->id }}">{{ $post->category->name}}</a>
        </p>


        
        <div>
            {!! $post->body !!}
        </div>
    </article>


    <a href="/">Go Back</a>
</x-layout>
   
```
```php

   <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;

    class Post extends Model
    {
    use HasFactory;

    protected $guarded =[];

    public function category()
    {
        return $this->belongsTo(Category::class);
    }

   
}
   
```
```php

   <?php

    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;



class Category extends Model
{

    use HasFactory;

    public function posts()
    {
        return $this->hasMany(Post::class);
    }
}
   
```