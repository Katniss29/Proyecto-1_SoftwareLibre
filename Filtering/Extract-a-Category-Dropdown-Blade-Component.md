- [Volver a las rutas](/Readme.md)

## Extract a Category Dropdown Blade Component

## Para este video realizamos varios cambios

### Nos permite edvolver una respuesta HTTP que incluye una vista Laravel, permitiendo asi la presentacion  de datos dinamicos en la intefaz de usuario.

```php
    
        return view('posts.index', compact('posts', 'categories', 'currentCategory'));


         return view('posts.show', compact('post'));
    
```

### El render juega un papel importante al proporcionar datos dinamicos a una vista de componente  en Laravel, permitiendo asi la creacion de interfaces de usuario interactivas y personalizables.


```php
    
    public function render()
    {
        $currentCategory = Category::firstWhere('slug', request('category'));

        return view('components.category-dropdown', [
            'categories' => Category::all(),
            'currentCategory' => $currentCategory ?? null,
        ]);
    }

    
```

### Creacion de un componente `category-dropdown`

```php
    
    <x-dropdown>
                <x-slot name="trigger">
                    <button class="py-2 pl-3 pr-9 text-sm font-semibold w-full lg:w-32 text-left flex lg:inline-flex">
                        {{ isset($currentCategory) ? ucwords($currentCategory->name) : 'Categories' }}

                        <x-icon name="down-arrow" class="absolute pointer-events-none" style="right: 12px;"/>
                    </button>
                </x-slot>

                <x-dropdown-item href="/" :active="request()->routeIs('home')">All</x-dropdown-item>

                @foreach ($categories as $category)
                    <x-dropdown-item
                        href="/?category={{ $category->slug }}"
                        :active='request()->is("categories/{$category->slug}")'
                    >{{ ucwords($category->name) }}</x-dropdown-item>
                @endforeach
</x-dropdown>
    
```

### Se llama al compontene `category-dropdown` en el archivo `_post-header

- `<x-category-dropdown/>`


### Se crea un carpeta llamada `posts` y se pasn los archivos:

- `_post-header`
- `posts.blade.php`
- `post.blade.php`


### Se renombran estos archivos a :

- `_header`
- `index`
- `show`

### Se cambia el llamado de `_post-header` a `_header` en `index`


- `@include('posts/_header')`