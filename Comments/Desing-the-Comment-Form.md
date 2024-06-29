## Desing the Comment Form

### Para este video creamos la caja de comentarios de los post para esto modificamos el archivo `show.balde.php`

- En este archivo agragamos la caja de comentarios con sus respectivos estilos ademas le agregamos le boton de postear de igual forma con sus respectivos estilos.

```php
            <form method="POST" action="#" class="border border-gray-200 p-6 rounded-xl">
                    @csrf

                    <header class="flex items-center">

                        <img src="https://i.pravatar.cc/60?u={{ auth()->id() }}" alt="" width="40" height="40" class="rounded-full">
                        <h2 class="ml-3">Want to participate?</h2>


                    </header>

                    <div class="mt-1">
                        <textarea name="body"  class="w-full text-sm focus:outline-none focus:ring"  rows="5" placeholder="Quick, thing of something to say !"></textarea>
                    </div>


                    <div class="flex justify-end mt-10 border-t border-gray-200 ">
                        <button  type="submit"class="bg-blue-500 text-white uppercase font-semibold text-xs py-2 px-10 rounded-2xl hover:bg-blue-600">Post</button>
                    </div>


                </form>

```

### Luego se crea el componente panel 

```php
    <div {{ $attributes(['class' => 'border border-gray-200 p-6 rounded-xl']) }}>
        {{ $slot }}
    </div>

```


### Y se modifica el archivo `post-comment` para utilizar el componente adecuadamente

```php

   @props(['comment'])

    <x-panel class="bg-gray-50">
        <article class="flex space-x-4">
            <div class="flex-shrink-0">
                <img src="https://i.pravatar.cc/60?u={{ $comment->user_id }}" alt="" width="60" height="60" class="rounded-xl">
            </div>
            
            <div>
                <header class="mb-4">
                    <h3 class="font-bold">{{ $comment->author->username }}</h3>

                    <p class="text-xs">
                        Posted
                        <time>{{ $comment->created_at->format('F j, Y, g:i a') }}</time>
                    </p>
                </header>
                <p>
                    {{ $comment->body }}
                </p>
            </div>
        </article>
    </x-panel>
```