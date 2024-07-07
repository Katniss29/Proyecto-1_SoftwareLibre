## Extend the Admin Layout 

- En este video agregamos estilos, agregamos componentes  y mejoramos las rutas.

- Ademas agregamos un nuevo componente llamado `setting.blade`

- Modificamos los create 

```php

@props(['name'])

<input class="border border-gray-200 p-2 w-full rounded"

{{ $attributes }}

```


```php
 class="border border-gray-200 p-2 w-full rounded"

  {{ $attributes }}
```

```php
    <x-dropdown>
                        <x-slot name="trigger">
                            <button class="text-xs font-bold uppercase">Welcome, {{ auth()->user()->name }}!</button>
                        </x-slot>

                        <x-dropdown-item href="/admin/dashboard">Dashboard</x-dropdown-item>
                        <x-dropdown-item href="/admin/posts/create" :active="request()->is('admin/posts/create')">New Post</x-dropdown-item>
                        <x-dropdown-item href="#" x-data="{}" @click.prevent="document.querySelector('#logout-form').submit()">Log Out</x-dropdown-item>

                        <form id="logout-form" method="POST" action="/logout" class="hidden">
                            @csrf
                        </form>
                    </x-dropdown> 

     <a href="/registers" class="text-xs font-bold uppercase {{ request()->is('register') ? 'text-blue-500' : '' }}">Register</a>
                    <a href="/loginn" class="ml-6 text-xs font-bold uppercase {{ request()->is('login') ? 'text-blue-500' : '' }}">Log In</a>
                    @endauth
```

```php
    @props(['heading'])

<section class="py-8 max-w-4xl mx-auto">
    <h1 class="text-lg font-bold mb-8 pb-2 border-b">
        {{ $heading }}
    </h1>

    <div class="flex">
        <aside class="w-48">
            <h4 class="font-semibold mb-4">Links</h4>

            <ul>
                <li>
                    <a href="/admin/dashboard" class="{{ request()->is('admin/dashboard') ? 'text-blue-500' : '' }}">Dashboard</a>
                </li>

                <li>
                    <a href="/admin/posts/create" class="{{ request()->is('admin/posts/create') ? 'text-blue-500' : '' }}">New Post</a>
                </li>
            </ul>
        </aside>

        <main class="flex-1">
            <x-panel>
                {{ $slot }}
            </x-panel>
        </main>
    </div>
</section>
```


```php
    <x-setting heading="Publish New Post">
        <form method="POST" action="/admin/posts" enctype="multipart/form-data">
            @csrf

            <x-form.input name="title"/>
            <x-form.input name="slug"/>
            <x-form.input name="thumbnail" type="file"/>
            <x-form.textarea name="excerpt"/>
            <x-form.textarea name="body"/>

    @foreach (\App\Models\Category::all() as $category)
                        <option
                            value="{{ $category->id }}"
                            {{ old('category_id') == $category->id ? 'selected' : '' }}
                        >{{ ucwords($category->name) }}</option>
                    @endforeach
```


```php
    <main class="max-w-lg mx-auto mt-10">
                <x-panel>
                    <h1 class="text-center font-bold text-xl">Register!</h1>

                    <form method="POST" action="/register" class="mt-10">
                        @csrf

                        <x-form.input name="name" />
                        <x-form.input name="username" />
                        <x-form.input name="email" type="email" />
                        <x-form.input name="password" type="password" autocomplete="new-password" />
                        <x-form.button>Sign Up</x-form.button>
                    </form>
                     </x-panel>
```


 ```php
     <main class="max-w-lg mx-auto mt-10">
                <x-panel>
                    <h1 class="text-center font-bold text-xl">Log In!</h1>
                    <form method="POST" action="/login" class="mt-10">
                    @csrf
                        <x-form.input name="email" type="email" autocomplete="username"/>
                        <x-form.input name="password" type="password" autocomplete="current-password"/>
                        <x-form.button>Log In</x-form.button>
                    </form>
    </x-panel>
 ```