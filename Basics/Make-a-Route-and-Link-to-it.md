- [Volver a las rutas](/Readme.md)

## Make a Route and Link to it 

Para este video se realizaton diferentes cambios en el proyecto el orden de los cambios fue el siguiente: 

## Orden


### 1. **Primero probamos ir a una ruta que no exite:** 
  
  - Para esto nos muestra una pantalla donde nos indica que la ruta no exite que si nos referimos a home.
  
### 2. **Le realizamos los siguientes cambios a `app.css`:**

```css
 body{
        background: white;
        color: #222222;
    }
``` 

### 3. **Luego le realizamos cambios a  `posts.bland.php`:**

  - Agregamos el primer post

```html
    <article>

        <h1>My First Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur,
             laborum temporibus blanditiis quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est labore velit.
        </p>

    </article>
 
``` 

### 4. **Le realizamos los siguientes cambios nuevamente a `app.css`:**

- Para darle un mejor estilo centrarlo y darle una tipografia.

```css
    body {

        background: white;

        color: #222222;

        max-width: 600px ; 

        margin: auto;

        font-family: sans-serif;
    }

    p {
        line-height: 1.6;
    }
```

### 5. **Se agraga un segundo post `posts.blade.php`:**


```html
    <article>

        <h1>My First Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur, laborum temporibus blanditiis
             quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est labore velit.
        </p>

    </article>

    <article>

        <h1>My First Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur, laborum temporibus blanditiis
             quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est labore velit.
        </p>

     </article>
``` 

### 6. **Se agraga estilo para se parar a un post de otro:**

```css

article + article {

    margin-top: 3rem;

    padding-top: 3rem;

    border-top: 1px solid #c5c5c5;
}
   
```

### 7. **Se crea una nueva ruta llamada `post`:**

```php
Route::get('post', function () {
    return view('post');
});
```

### 8. **Se crea un nuevo archivo llamado `post.blade.php`:** 
   
- Esto con el fin de porder ulizar la ruta correctamente


### 9. **Se agragran enlaces a los `post` que se encuentan en `posts.blade.php`:** 
   
 - Esto con el fin de rederigir los enlaces al archivo antes creado llamado `post`

```html
    <article>

        <h1><a href="/post">My First Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas aspernatur, laborum temporibus blanditiis
             quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est labore velit.
        </p>

    </article>
```

### 10. **Se agrega codigo al archivo `post.blade.php`:** 
   


```html
   <!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
    <article>

        <h1><a href="/post">My First Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Iure, dolorem? Repellat culpa quas 
            aspernatur, laborum temporibus blanditiis quos omnis veniam fugiat obcaecati expedita unde odit exercitationem consequatur est labore velit.
        </p>

    </article>
    
    <a href="/">Go Back</a>
</body>
```

### 11. **Se agrega codigo al archivo `post.blade.php` una etiqueta `a` para volver a la pagina `posts`:** 
    
```html
<a href="/">Go Back</a>

```


