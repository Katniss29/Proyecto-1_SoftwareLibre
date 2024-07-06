## Toy Chests and Contracts 

## Para este video relizamos los siguientes pasos

### 1 - Utilizamos como obejto registrar una implementación de interfaz `Newsletter` utilizando el servicio de Mailchimp

 ```php
    use App\Services\MailchimpNewsletter;
    use Illuminate\Support\ServiceProvider;
    use Illuminate\Database\Eloquent\Model;

    class AppServiceProvider extends ServiceProvider
        */
        public function register()
        {
            //
            app()->bind(Newsletter::class, function () {
                $client = (new ApiClient)->setConfig([
                    'apiKey' => config('services.mailchimp.key'),
                    'server' => 'us6'
                ]);

                return new MailchimpNewsletter($client);
            });
        }
```


### 2 - Creamos un nuevo servicio llamado `ConvertNewsletter` el cual se encarga de implementar la interfaz `Newsletter el cual define un metodo `subscribe` que toma un email y una lista opcional como parámetros.

 ```php
   <?php

    namespace App\Services;



    class ConvertKitNewsletter implements Newsletter
    {
        public function subscribe(string $email, string $list = null)
        {

        }

    }
   ```

### 3 - Definimos una clase `MailchimpNewsletter` que implementa la interfaz de `Newsletter` y  porporciona funcionalidad para suscribir usuarios a una lista de correo usando Mailchimp.

 ```php
   <?php

    namespace App\Services;

    use MailchimpMarketing\ApiClient;

    class MailchimpNewsletter implements Newsletter
    {

        public function __construct(protected ApiClient $client, protected string $foo), 
        {

        }

        public function subscribe(string $email, string $list = null)
        {
            $list ??= config('services.mailchimp.lists.subscribers');

            return $this->client()->lists->addListMember($list, [
                'email_address' => $email,
                'status' => 'subscribed'
            ]);
        }


    }
```

