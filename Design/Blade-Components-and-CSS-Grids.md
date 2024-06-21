##  Blade Components and CSS Grids

## Mejoras al Codigo

### Post blade

```php
    <x-layout>
        @include('_post-header') 

        <main class="max-w-6xl mx-auto mt-6 lg:mt-20 space-y-6">
            @if ($posts->count())
            <x-posts-grid :posts="$posts" />
            @else
                <p class="text-center">No posts yet. Please check back later.</p>
            @endif
        </main>
    </x-layout>

```

- Este codigo muestra un diseño de pagina que incluye el ` _post-header`, una pantilla en espeficico para ver las publicaciones y un componente `posts-grid` para mostrar en forma de cuadricula las publicaciones.


### post card


```php
    @props(['post'])

    <article
        {{ $attributes->merge(['class' => 'transition-colors duration-300 hover:bg-gray-100 border border-black border-opacity-0 hover:border-opacity-5 rounded-xl']) }}>
        <div class="py-6 px-5 lg:flex">
            <div class="flex-1 lg:mr-8">
                <img src="/images/illustration-1.png" alt="Blog Post illustration" class="rounded-xl">
            </div>

            <div class="flex-1 flex flex-col justify-between">
                <header class="mt-8 lg:mt-0">
                    <div class="space-x-2">
                        <a href="/categories/{{ $post->category->slug }}"
                        class="px-3 py-1 border border-blue-300 rounded-full text-blue-300 text-xs uppercase font-semibold"
                        style="font-size: 10px">{{ $post->category->name }}</a>
                    </div>

                    <div class="mt-4">
                        <h1 class="text-3xl">
                            <a href="/posts/{{$post->slug}}">
                                {{ $post->title }}
                            </a>
                        </h1>

                        <span class="mt-2 block text-gray-400 text-xs">
                            Published <time>{{ $post->created_at->diffForHumans() }}</time>
                        </span>
                    </div>
                </header>

                <div class="text-sm mt-2">
                    <p>
                        {{ $post->excerpt }}
                    </p>
                </div>

                <footer class="flex justify-between items-center mt-8">
                    <div class="flex items-center text-sm">
                        <img src="./images/lary-avatar.svg" alt="Lary avatar">
                        <div class="ml-3">
                            <h5 class="font-bold">{{ $post->author->name }}</h5>
                            <h6>Mascot at Laracasts</h6>
                        </div>
                    </div>

                    <div class="hidden lg:block">
                        <a href="/posts/{{ $post->slug }}"
                        class="transition-colors duration-300 text-xs font-semibold bg-gray-200 hover:bg-gray-300 rounded-full py-2 px-8"
                        >Read More</a>
                    </div>
                </footer>
            </div>
        </div>
    </article>


```

- Este componente crea una estrutura visualmente atractiva para mostrar las diferentes partes de la publicacion por ejemplo `articulo`, `imagen`, `titulo`, `categoria`, `fehca de publicacion`, `informacion del autor`, `y enlace para leer mas`.


### post featured card


```php

   @props(['post'])

    <article {{ $attributes->merge(['class' => 'transition-colors duration-300 hover:bg-gray-100 border border-black border-opacity-0 hover:border-opacity-5 rounded-xl']) }}>
        <div class="py-6 px-5 lg:flex">
            <div class="flex-1 lg:mr-8">
                {{-- Imagen de ilustración --}}
                <img src="/images/illustration-1.png" alt="Blog Post illustration" class="rounded-xl">
            </div>

            <div class="flex-1 flex flex-col justify-between">
                <header class="mt-8 lg:mt-0">
                    <div class="space-x-2">
                        {{-- Enlace a la categoría --}}
                        <a href="/categories/{{ $post->category->slug }}"
                        class="px-3 py-1 border border-blue-300 rounded-full text-blue-300 text-xs uppercase font-semibold"
                        style="font-size: 10px">{{ $post->category->name }}</a>
                    </div>

                    <div class="mt-4">
                        {{-- Título del post --}}
                        <h1 class="text-3xl">
                            <a href="/posts/{{$post->slug}}">
                                {{ $post->title }}
                            </a>
                        </h1>

                        {{-- Fecha de publicación --}}
                        <span class="mt-2 block text-gray-400 text-xs">
                            Published <time>{{ $post->created_at->diffForHumans() }}</time>
                        </span>
                    </div>
                </header>

                <div class="text-sm mt-2">
                    {{-- Extracto del post --}}
                    <p>{{ $post->excerpt }}</p>
                </div>

                <footer class="flex justify-between items-center mt-8">
                    <div class="flex items-center text-sm">
                        {{-- Avatar del autor --}}
                        <img src="./images/lary-avatar.svg" alt="Lary avatar">
                        <div class="ml-3">
                            {{-- Nombre del autor --}}
                            <h5 class="font-bold">{{ $post->author->name }}</h5>
                            {{-- Rol del autor --}}
                            <h6>Mascot at Laracasts</h6>
                        </div>
                    </div>

                    <div class="hidden lg:block">
                        {{-- Botón para leer más --}}
                        <a href="/posts/{{ $post->slug }}"
                        class="transition-colors duration-300 text-xs font-semibold bg-gray-200 hover:bg-gray-300 rounded-full py-2 px-8"
                        >Read More</a>
                    </div>
                </footer>
            </div>
        </div>
    </article>


```


- Al igual que el anterior este componente crea una estrutura visualmente atractiva para mostrar un post. Por otro lado se utiliza `{{}}` para mostrar datos especificos del post.