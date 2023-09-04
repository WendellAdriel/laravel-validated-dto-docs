# Introduction

You can easily cast your DTO properties by defining a casts method in your DTO:

```php
/**
 * Defines the type casting for the properties of the DTO.
 *
 * @return array
 */
protected function casts(): array
{
    return [
        'name' => new StringCast(),
        'age'  => new IntegerCast(),
        'created_at' => new CarbonImmutableCast(),
    ];
}
```
