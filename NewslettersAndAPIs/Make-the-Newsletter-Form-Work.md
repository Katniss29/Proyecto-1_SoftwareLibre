## Make the Newsletter Form Work

## Para este video agregamos la ruta en un post y le pusimos excepciones


```php

  Route::post('newsletter', function (Request $request) {
    $request->validate(['email' => 'required|email']);

    $mailchimp = new ApiClient();

    $mailchimp->setConfig([
        'apiKey' => config('services.mailchimp.key'),
        'server' => config('services.mailchimp.server')
    ]);

    try {
        $response = $mailchimp->lists->addListMember(config('services.mailchimp.lists.subscribers'), [
            'email_address' => $request->email,
            'status' => 'subscribed'
        ]);

        return redirect('/')->with('success', 'You are now signed up for our newsletter!');
    } catch (\Exception $e) {
        return redirect('/')->with('error', 'Failed to subscribe: ' . $e->getMessage());
    }
});
  

```