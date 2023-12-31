# Configuration

Publish the config file:

```
php artisan vendor:publish --provider="WendellAdriel\ValidatedDTO\Providers\ValidatedDTOServiceProvider" --tag=config
```

The configuration file will look like this:

```php
<?php

return [

    /*
    |--------------------------------------------------------------------------
    | NAMESPACE
    |--------------------------------------------------------------------------
    |
    | The namespace where your DTOs will be created.
    |
    */

    'namespace' => 'App\\DTOs',

    /*
    |--------------------------------------------------------------------------
    | REQUIRE CASTING
    |--------------------------------------------------------------------------
    |
    | If this is set to true, you must configure a cast type for all properties of your DTOs.
    | If a property doesn't have a cast type configured it will throw a
    | \WendellAdriel\ValidatedDTO\Exceptions\MissingCastTypeException exception
    |
    */

    'require_casting' => false,
];
```
