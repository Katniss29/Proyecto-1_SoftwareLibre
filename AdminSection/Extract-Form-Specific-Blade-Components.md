## Extract Form Specific Blade Components

- Para este video se estructuro en componentes para mantener el codigo limpio.


- Creamos un folder `form` donde agregamos los diferentes archivos que estructuran el form  

```php
    <x-form.field>
    <button type="submit"
            class="bg-blue-500 text-white uppercase font-semibold text-xs py-2 px-10 rounded-2xl hover:bg-blue-600"
    >
        {{ $slot }}
    </button>
</x-form.field>

```

```php
@props(['name'])

@error($name)
    <p class="text-red-500 text-xs mt-2">{{ $message }}</p>
@enderror


```
```php
<div class="mt-6">
    {{ $slot }}
</div>

```


```php
@props(['name', 'type' => 'text'])

<x-form.field>
    <x-form.label name="{{ $name }}"/>
 <input class="border border-gray-400 p-2 w-full"
           type="{{ $type }}"
           name="{{ $name }}"
           id="{{ $name }}"
           value="{{ old($name) }}"
           required
           >
     <x-form.error name="{{ $name }}"/>
    </x-form.field>
```

```php
@props(['name'])

<label class="block mb-2 uppercase font-bold text-xs text-gray-700"
       for="{{ $name }}"
>
    {{ ucwords($name) }}
</label>
```

```php
@props(['name'])

<x-form.field>
    <x-form.label name="{{ $name }}" />

    <textarea
        class="border border-gray-400 p-2 w-full"
        name="{{ $name }}"
        id="{{ $name }}"
        required
    >{{ old($name) }}</textarea>

    <x-form.error name="{{ $name }}" />
</x-form.field>
```

```php
<x-form.button>Submit</x-form.button>
```

```php
    <x-form.input name="title" />
    <x-form.input name="slug" />
    <x-form.input name="thumbnail" type="file" />
    <x-form.textarea name="excerpt" />
    <x-form.textarea name="body" />

    <x-form.field>
                <x-form.label name="category" />

    <select name="category_id" id="category_id">

    </select>

        <x-form.error name="category" />
        </x-form.field>

  <x-form.button>Publish</x-form.button>       

```














