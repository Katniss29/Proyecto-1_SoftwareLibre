## Table Consistency and Foreing Key Constraints 

### Para este video se creo el Model de Comments 

- `php artisan make:model Comment -mfc`

- Y se agregan los atributos que se necesitan para el `migratión`

```php

    <?php

    use Illuminate\Database\Migrations\Migration;
    use Illuminate\Database\Schema\Blueprint;
    use Illuminate\Support\Facades\Schema;

    class CreateCommentsTable extends Migration
    {
        /**
         * Run the migrations.
         *
         * @return void
         */
        public function up()
        {
            Schema::create('comments', function (Blueprint $table) {
                $table->id();
                $table->foreignId('post_id')->constrained()->cascadeOnDelete();
                $table->foreignId('user_id')->constrained()->cascadeOnDelete();
                $table->text('body');
                $table->timestamps();
            });
        }

        /**
         * Reverse the migrations.
         *
         * @return void
         */
        public function down()
        {
            Schema::dropIfExists('comments');
        }
    }

```

### Se agrega

- `$table->foreignId('user_id')->constrained()->cascadeOnDelete();`

- `constrained`  defibe la restriccion de clave foránea y  establece las convenciones de nombre predeterminadas para la tabla y columna referenciadas y `cascadeOnDelete`  define la acción de eliminacion en cascada, asegurando que los registros relacionados se eliminen automáticamente cuando se elimine el registro principal en la tabla referenciada.