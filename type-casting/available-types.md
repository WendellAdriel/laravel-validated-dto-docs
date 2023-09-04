# Available Types

### Array <a href="#array" id="array"></a>

For JSON strings, it will convert into an array, for other types, it will wrap them in an array.

```php
protected function casts(): array
{
    return [
        'property' => new ArrayCast(),
    ];
}
```

### Boolean <a href="#boolean" id="boolean"></a>

For string values, this uses the `filter_var` function with the `FILTER_VALIDATE_BOOLEAN` flag.

```php
protected function casts(): array
{
    return [
        'property' => new BooleanCast(),
    ];
}
```

### Carbon <a href="#carbon" id="carbon"></a>

This accepts any value accepted by the `Carbon` constructor. If an invalid value is found it will throw a `\WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonCast(),
    ];
}
```

You can also pass a timezone when defining the cast if you need that will be used when casting the value.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonCast('Europe/Lisbon'),
    ];
}
```

You can also pass a format when defining the cast to be used to cast the value. If the property has a different format than the specified it will throw a `\WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonCast('Europe/Lisbon', 'Y-m-d'),
    ];
}
```

### CarbonImmutable <a href="#carbonimmutable" id="carbonimmutable"></a>

This accepts any value accepted by the `CarbonImmutable` constructor. If an invalid value is found it will throw a `\WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonImmutableCast(),
    ];
}
```

You can also pass a timezone when defining the cast if you need that will be used when casting the value.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonImmutableCast('Europe/Lisbon'),
    ];
}
```

You can also pass a format when defining the cast to be used to cast the value. If the property has a different format than the specified it will throw a `\WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new CarbonImmutableCast('Europe/Lisbon', 'Y-m-d'),
    ];
}
```

### Collection <a href="#collection" id="collection"></a>

For JSON strings, it will convert into an array first, before wrapping it into a `Collection` object.

```php
protected function casts(): array
{
    return [
        'property' => new CollectionCast(),
    ];
}
```

If you want to cast all the elements inside the `Collection`, you can pass a `Castable` to the `CollectionCast` constructor. Let's say that you want to convert all the items inside the `Collection` into integers:

```php
protected function casts(): array
{
    return [
        'property' => new CollectionCast(new IntegerCast()),
    ];
}
```

This works with all `Castable`, including `DTOCast` and `ModelCast` for nested data.

### DTO <a href="#dto" id="dto"></a>

This works with arrays and JSON strings. This will validate the data and also cast the data for the given DTO.

This will throw a `Illuminate\Validation\ValidationException` exception if the data is not valid for the DTO.

This will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception if the property is not a valid array or valid JSON string.

This will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastTargetException` exception if the class passed to the `DTOCast` constructor is not a `ValidatedDTO` instance.

```php
protected function casts(): array
{
    return [
        'property' => new DTOCast(UserDTO::class),
    ];
}
```

### Float <a href="#float" id="float"></a>

If a not numeric value is found, it will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new FloatCast(),
    ];
}
```

### Integer <a href="#integer" id="integer"></a>

If a not numeric value is found, it will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new IntegerCast(),
    ];
}
```

### Model <a href="#model" id="model"></a>

This works with arrays and JSON strings.

This will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception if the property is not a valid array or valid JSON string.

This will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastTargetException` exception if the class passed to the `ModelCast` constructor is not a `Model` instance.

```php
protected function casts(): array
{
    return [
        'property' => new ModelCast(User::class),
    ];
}
```

### Object <a href="#object" id="object"></a>

This works with arrays and JSON strings.

This will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception if the property is not a valid array or valid JSON string.

```php
protected function casts(): array
{
    return [
        'property' => new ObjectCast(),
    ];
}
```

### String <a href="#string" id="string"></a>

If the data can't be converted into a string, this will throw a `WendellAdriel\ValidatedDTO\Exceptions\CastException` exception.

```php
protected function casts(): array
{
    return [
        'property' => new StringCast(),
    ];
}
```
