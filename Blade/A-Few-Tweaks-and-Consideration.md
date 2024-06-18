- [Volver a las rutas](/Readme.md)

## A few Tweaks and Consideration 

- Para este video realizamos modificaiones en el archivo `post` y le implementamos la plantilla de `layout` 

```php
    <x-layout>
        <article>
            <h1>{{ $post->title }}</h1>
            <div>
                {!! $post->body !!}
            </div>
        </article>
        <a href="/">Go Back</a>
    </x-layout>
```


- Luego de esto implementamos una funcion en post para las `url` no existentes.

```php
    public static function find($slug){
        
        return static::all()->firstWhere('slug', $slug);

        
            
            
        }

        public static function findOrFail($slug){
        
            $post =  static::find($slug);
    
            if (! $post) {
    
            throw new ModelNotFoundException();
            }
    
            return $post;
            
             
         }

```

- Y modificamos el archivo `web` para el funcionamiento correcto de las rutas

```php
    Route::get('posts/{post}', function ($slug) {

        return view('post', [
            'post' =>  Post::findOrFail($slug)
        ]);
    });
```


   