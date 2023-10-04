# Introduction

You can easily cast your DTO properties by defining a casts method in your DTO:

```php
protected function casts(): array
{
    return [
        'name' => new StringCast(),
        'age'  => new IntegerCast(),
        'created_at' => new CarbonImmutableCast(),
    ];
}
```

If you don't want to cast any of the properties, you can use the `EmptyCasts` trait to avoid having to define the `casts()` method.

```php
use WendellAdriel\ValidatedDTO\Concerns\EmptyCasts;

class UserDTO extends ValidatedDTO
{
    use EmptyCasts;

    public string $name;

    public string $email;
}
```
