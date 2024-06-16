## Store Blog Posts as HTML Files 

Para este video creamos una escructura de archivos por post para esto seguimos los siquientes pasos.

## Pasos 

### 1. **Cambiar el archivo de  `post`:** 

- Para esto eliminamos el post quemado que teniamos y colocamos lo siguiente

```html 
<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
    <article>

       <?= $post; ?>

    </article>
    
    <a href="/">Go Back</a>
</body>

```

Esto lo que permite es mostrar el post quese esta mandando por la ruta y no mostrar codigo quemado.


### 2. **Cambiar el archivo de  `web`:** 

- En web cambiamos las rutas para poder renderizar a los archivos que necesitemos

```php

    Route::get('posts/{post}', function ($slug) {
    
    
    $path =  _DIR_ . "/../resources/posts/{$slug}.html";

    if(! file_exists($path)) {
        
        //dd('file does not exists');

        //ddd('file does not exists');

        //abort(404);

        return redirect('/');


    }

    $post = file_get_contents($path);

    return view('post', [
        'post' => $post
        
    ]);
    
});
```

Como podemos observar tenemos una ruta establecidad con posts/post que es el post que recibe el archivo post para mostrar el post que deseamos, luego tenemos un parametro llamo `$slug` que es el encargado de traer el post seleccionado por el usuario, despues de esto ubicamos la ruta para renderizar al la url correcta, el condicional que existe son diferentes maneras de mostrar que el sitio no exite, y el `redirect` es para dirigirse a la pagina raiz si no se encuentra ningun sitio.


### 3. **Crear los diferentes archivos posts:** 

- Para este punto solamente una carpeta llamada `posts` y en ella  creamos 3 archivos .html donde insertamos el codigo de los post que ya habiamos echo anteriormente, para que cada post tenga su propio contenido.
  



### 4. **Modificar los posts con la ruta correcta:** 

- Ejemplo

```php

<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
    <article>

        <h1><a href="/posts/my-first-post">My First Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur, 
            laborum temporibus blanditiis quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est 
            labore velit.
        </p>

    </article>

    <article>

        <h1><a href="/posts/my-second-post">My Second Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur, 
            laborum temporibus blanditiis quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est 
            labore velit.
        </p>

    </article>
</body>
```