- [Volver a las rutas](/Readme.md)

## Find a Composer Package for Post Metadata

### **Para este video empezamos instalando :**  

- `yaml-front-matter`

- Se refiere a un bloque de metadatos al inicio de un archivo.
- Este bloque se encuentra delimitado por tres guiones bajos al inicio y al final del archivo y se utiliza para definir variables y configuraciones asociadas al contenido del archivo, como titulo y fecha.

### **Se modifica el archivo `web.php` y modificamos la ruta principal :** 

- Utilizando `yaml-front-matter`

```php

Route::get('/', function () {
    $document = YamlFrontMatter::parseFile(
        resource_path('posts/my-fourth-post.html')

    );

    ddd ($document);
});

```

### **Se modifica el archivo `Post` creando atributos y un constructor:** 

```php
public $title;

    public $excerpt;

    public $date;


    public $body; 

    public $slug;

    public function __construct($title, $excerpt, $date, $body, $slug)
    {

        $this->title = $title;
        $this->excerpt = $excerpt; 
        $this->date = $date; 
        $this->body = $body; 
        $this->slug = $slug; 


    }

```


### **Luego modificamos la funcion `all`:**

- Esta funcion  obtiene todos los archivos en el directorio `posts`, analiza el contenido `YAML` de cada archivo y crea instancias de la clase `Post` .

```php
public static function all()
    {

        return collect(File::files(resource_path("posts")))
            ->map(fn($file) => YamlFrontMatter::parseFile($file))
            ->map(fn($document) => new Post(
                $document->title,
                $document->excerpt,
                $document->date,
                $document->body(), 
                $document->slug
        ));    

     
    }

```

### **Se modifica la funcion `find`:**

- Esta funcion devuleve el post correspondiente al `slug` especificado o `null` si no se encuentra ninguno.


### **Se modifica el archivo `posts`:**

- Esta modificacion renderiza una lista de publicaciones ennun blog dinamico con php.


```php

<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>

    <?php foreach ($posts as $post) : ?> 

        <article>

            <h1>
                <a href="/posts/<?= $post->slug; ?>">
                    <?= $post->title; ?>
                </a>
            
            </h1>

            <div>
                <?= $post->excerpt; ?>
            </div>
            

        </article>

    <?php endforeach; ?>
    
</body>

```

### **Se modifica el archivo `post`:**

- Esta modificacion es util para visualizar una publicacion especifica de manera detallada en un blog, permitiendo a lso usuarios leer contenido completo y navegar facilmente de vuelta a la lista de publicaciones.

```php
<!doctype html> 

<title>My Blog</title>
 <link rel="stylesheet" href="/app.css">


<body>
    <article>

        <h1> <?= $post->title; ?></h1>

        <div>
            <?= $post->body; ?>
        </div>
      

    </article>
    
    <a href="/">Go Back</a>
</body>
```

###  **Por ultimo modificamos las rutas**

- Este esquema basico de las rutas proporciona una estructura inicial para el blog, permite visualizar y navegar entre las publicaciones.

```php
Route::get('/', function () {
  
    return view('posts', [
        'posts' => Post::all()
    ]); 
});


Route::get('posts/{post}', function ($slug) {
    // Find a post by its slug and pass it to a view called "post"
    return view('post', [
        'post' => Post::find($slug) // Aquí se eliminó el punto y coma incorrecto
    ]);
})->where('post', '[A-z_\-]+');

Auth::routes();

Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

```