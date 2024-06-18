- [Volver a las rutas](/Readme.md)

## Turbo Boots With Factories

## Pasos para el video

### 1. En linea de comandos ejecutamos el siguiente comando  `App\Models\User::factory(3)->create();`

- Esto lo que permite es crear usuarios random, en este caso el 3 es la cantidad de usarios que le solicito.

### 2.  En linea de comandos ejecutamos el siguiente comando  `App\Models\Post::factory(50)->create();`

- Esto lo que permite es crear Post random, en este caso el 50 es la cantidad de usarios que le solicito.

- Para los post existieron algunas dificultades para esto tuvimos que hacer  lo siguiente: 
 
    - Crear un archivo  `PostFactory`
    - Modificar ese archivo 
    - ```php
            public function definition()
            {
                return [
                    'user_id' => Category::factory(),
                    'category_id' => Category::factory(),
                    'title' => $this->faker->sentence,
                    'slug' => $this->faker->slug,
                    'excerpt' => $this->faker->sentence,
                    'body' => $this->faker->paragraph
              ];
            }
        }
        ```

    - Crear un archivo  `CategoryFactory`: 
    - Modificar ese archivo 
    - ```php
        class CategoryFactory extends Factory
        {
            public function definition()
            {
                return [
                    'name' => $this->faker->word,
                    'slug' => $this->faker->slug
              ];
            }
        }
    ```

### 3. **Modificar el archivo DatabaseSeeder**

- ```php
  User::truncate();
        Category::truncate();
        Post::truncate();


        Post::factory()->create(); 
```