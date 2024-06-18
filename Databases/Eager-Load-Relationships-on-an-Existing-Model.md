- [Volver a las rutas](/Readme.md)

## Eager Load Relationships on an Existing


- Para este video se realizaron muchas pruebas con clockwork y algunos cambios en el codigo.
- Los cambios son los siguientes:


```php
   class Post extends Model
    {
    use HasFactory;

    protected $guarded = [];

    protected $with = ['category', 'author'];

    public function category(): BelongsTo
    {
        return $this->belongsTo(Category::class);
    }

    public function author(): BelongsTo
    {
        return $this->belongsTo(User::class, 'user_id');
    }
```


```php
  Route::get('/', function () {

  
    return view('posts', [
        'posts' => Post::latest()->get()
    ]); 
});


Route::get('posts/{post:slug}', function (Post $post) {

    return view('post', [
        'post' =>  $post
    ]);
});
```