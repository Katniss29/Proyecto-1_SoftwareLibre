## How to Extract a Dropdown Blade Component


## Para este video trabajamos diferentes archivos 

### Creacion de los siguientes archivos 

- `dropdown-item.blade.php`
- `dropdown.blade.php`
- `icon.blade.php`


### dropdown-item.blade.php


```php

    @props(['active' => false])

    @php
        $classes = 'block text-left px-3 text-sm leading-6 hover:bg-blue-500 focus:bg-blue-500 hover:text-white focus:text-white';
        if ($active) $classes .= ' bg-blue-500 text-white';
    @endphp

    <a {{ $attributes(['class' => $classes]) }}
    >{{ $slot }}</a>

```

- Este componente permite crear enlances `<a>` con nclases dinamicas dependiendo de si estan activos o no. Esto facilita la creacion de menus o listas de navegacion donde se necesita resaltar el elemento activo visualmente.

### dropdown.blade.php


```php

    @props(['trigger'])

    <div x-data="{ show: false }" @click.away="show = false">
        {{-- Trigger --}}
        <div @click="show = ! show">
            {{ $trigger }}
        </div>

        {{-- Links --}}
        <div x-show="show" class="py-2 absolute bg-gray-100 mt-2 rounded-xl w-full z-50" style="display: none">
            {{ $slot }}
        </div>
    </div>

```

- Este componente crea un menu desplegable que se activa cuando se hace click en un elemento especifico `$trigger`. Utiliza `Alpine.js` para gestionar el estado de visibilidad del menu, proporcionando una interaccion suave y sin necesidad de recargar la pagina.


### icon.blade.php


```php
    @props(['name'])

    @if ($name === 'down-arrow')
        <svg {{ $attributes(['class' => 'transform -rotate-90']) }} width="22" height="22" viewBox="0 0 22 22">
            <g fill="none" fill-rule="evenodd">
                <path stroke="#000" stroke-opacity=".012" stroke-width=".5" d="M21 1v20.16H.84V1z">
                </path>
                <path fill="#222"
                    d="M13.854 7.224l-3.847 3.856 3.847 3.856-1.184 1.184-5.04-5.04 5.04-5.04z"></path>
            </g>
        </svg>
    @endif

```

- Este componente verifica si la propiedad `$name` es igual a `down-arrow` si es asi, renderisza un icono SVG que representa una flecha hacia abajo. Esta tecnica permite crear componentes reutilizables que pueden mostrar diferentes iconos basados en las propiedades proporcionadas, lo que es util para construir interfaces dinamicas y personalizables.

### Finalmente se agregan estos componentes al archivo '_post-header'.