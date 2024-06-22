## Quick Tweak and Clean Up 

### Para este video trabajamos varios archivos.

- `CategoryFactory.php`.
- `PostFactory.php`.
- `post-card.blade.php`.
- `post-featured-card.blade.php`.
- `post.blade.php`.


### CategoryFactory.php


```php

    <?php

    namespace Database\Factories;


    use App\Models\Category;
    use App\Models\Post;
    use App\Models\User;


    use Illuminate\Database\Eloquent\Factories\Factory;

    class CategoryFactory extends Factory
    {
        /**
         * Define the model's default state.
         *
         * @return array
         */
        public function definition()
        {
            return [
                'name' => $this->faker->word,
                'slug' => $this->faker->slug,
          ];
        }
    }
  
```

- Este codigo configura los datos para el modelo `Category`, que genera datos de prueba realistas para las categorias.


### PostFactory.php



```php

   <?php


    namespace Database\Factories;


    use App\Models\Post;
    use App\Models\User;
    use App\Models\Category;
    use Illuminate\Database\Eloquent\Factories\Factory;

    class PostFactory extends Factory
    {
        /**
         * Define the model's default state.
         *
         * @return array
         */
        public function definition()
        {
            return [
                'user_id' => Category::factory(),
                'category_id' => Category::factory(),
                'title' => $this->faker->sentence,
                'slug' => $this->faker->slug,
                'excerpt' => '<p>' . implode('</p><p>', $this->faker->paragraphs(2)) . '</p>',
                'body' => '<p>' . implode('</p><p>', $this->faker->paragraphs(6)) . '</p>',
          ];
        }
    }

```

- Este codigo configura los datos para el modelo `Post`, que genera datos de prueba realistas para los posts.



### post-card.blade.php


```php

    <div class="text-sm mt-2 space-y-4">
        {!! $post->excerpt !!}
     </div>

```

- Se le agrega este fragmento de codigo para mostrar el `excerpt`


### post-featured-card.blade.php


```php

    <div class="text-sm mt-2 space-y-4">
        {!! $post->excerpt !!}
     </div>

```

- Se le agrega este fragmento de codigo para mostrar el `excerpt`


