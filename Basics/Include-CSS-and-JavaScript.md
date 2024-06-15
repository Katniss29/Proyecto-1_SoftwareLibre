## Include CSS and JavaScript

En este video, realizamos cambios en el archivo `welcome.blade.php`, donde borramos todo el HTML por defecto y realizamos los siguientes cambios:


### 1. Creación de `nuevo código`:

- Se inicia un nuevo código HTML:

    ```html
    <!doctype html> 
    <title>My Blog</title>
    <body>
        <h1>Hello Word</h1>
    </body>
    ```
### 2. Se crea un  `archivo app.css`:

- En este archivo apregamos un background-color y un color 
    ```css
    body{
        background-color: navy;
        color: white;
    }
    ```

### 3. Se crea un `archivo app.js`:

- Donde se agrega un `alert`

    ```JavaScript
    alert('I am here');
    ```

### 4. Se agraga el link y el script de css y js

- Para ver los cambios en Welcome agragamos las etiquetas de `link` y  `script`

    ```html
    <!doctype html> 

    <title>My Blog</title>
    <link rel="stylesheet" href="/app.css">
    <script src="/app.js"></script>

    <body>
        <h1>Hello Word</h1>
    </body>
    ```





