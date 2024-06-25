- [Volver a las rutas](/Readme.md)

## Search (The Messy Way)

## Para este video modificamos varios archivos

### Se modifica el archivo `CategoryController`

```php

    public function index()
    {
        $posts = Post::latest();

        if (request('search')) {
            $posts
            ->where('title', 'like', '%' . request('search') . '%')
            ->orWhere('body', 'like', '%' . request('search') . '%');
        }

        $posts = $posts->get(); // Agregar el método get() al final para ejecutar la consulta y obtener los resultados

        $categories = Category::all();

        return view('posts', compact('posts', 'categories'));
    }
}

```

- Este codigo permite llevar el Query que se necesita para realizar la busquedad

### Se modifica el archivo `_post-header`


```php

    <div class="relative flex lg:inline-flex items-center bg-gray-100 rounded-xl px-3 py-2">
            <form method="GET" action="#">
                <input type="text"
                       name="search"
                       placeholder="Find something"
                       class="bg-transparent placeholder-black font-semibold text-sm"
                       value="{{ request('search') }}"
                >
            </form>
    </div>

```

- Este fraqmento de codigo crea un campo de busqueda funcional que permite a lso usuarios ingresar terminos de busqueda y enviar al formulario utilizando el metodo `GET`

