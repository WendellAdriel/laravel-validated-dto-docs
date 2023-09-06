# Upgrade Guide

I tried to maintain backward compatibility as much as possible, but there are some breaking changes while
upgrading from v2 to v3.

## PHP version

The minimum PHP version required is now 8.1.

## Configuration

If you published the config file before, or if you want to customize the path/namespace used to generate your DTOs,
you'll need to merge the new config file with your old one or publish it. This is the new config file:

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

## Mapping DTO data

The methods used to map the DTO data were renamed to be more accurate:

- `mapBeforeValidation()` was renamed to `mapData()`
- `mapBeforeExport()` was renamed to `mapToTransform()`

## Transforming the DTO

If you're using the `->toJson()` method passing `true` as argument to transform it to a formatted JSON string, you'll
need to use the `->toPrettyJson()` method instead, since the `->toJson()` method now returns a JSON string without any
formatting.
