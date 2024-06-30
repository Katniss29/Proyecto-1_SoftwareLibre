## Mailchip API Tinkering 

## Para este video empezamos a ver el funcionamiento de las APIS 

### Para esto nos inscribimos en la pagina de `Mailchimp` el cual es una app para mandar correos electronico que tiene un plan gratis de 50 correos 

### Instalamos `Mailchimp`

- `"mailchimp/marketing": "^3.0",`

### Establecer las configuraciones necesarias para interactuar con la API de Mailchimp, obteniendo las credenciales y IDs de listas desde variables de entorno

```php

   'mailchimp' => [
        'key' => env('MAILCHIMP_KEY'),
        'lists' => [
            'subscribers' => env('MAILCHIMP_LIST_SUBSCRIBERS')
        ]
    ] 

```

### Agregamos la ruta a web para el buen funcionamiento con manejo de excepciones

```php
   Route::get('ping', function (){

    $mailchimp = new \MailchimpMarketing\ApiClient();

    $mailchimp->setConfig([
        'apikey' => config('services.mailchimp.key'),
        'server' => 'us13'
    ]);

    $response = $mailchimp->lists->addListMember('d3c0c95629', [
        'email_address' => 'arceemi29@gmail.com',
        'status' => 'subscribed'
    ]);

    ddd($response);


})
```