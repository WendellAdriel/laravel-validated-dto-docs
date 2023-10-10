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

Alternatively, for simpler cases, you can use the `Cast` attribute:

```php
use WendellAdriel\ValidatedDTO\Attributes\Cast;
use WendellAdriel\ValidatedDTO\Concerns\EmptyCasts;

class UserDTO extends ValidatedDTO
{
    use EmptyCasts;

    public string $name;

    public string $email;

    #[Cast(BooleanCast::class)]
    public bool $active;

    #[Cast(IntegerCast::class)]
    public ?int $age;

    #[Cast(type: ArrayCast::class, param: FloatCast::class)]
    public ?array $grades;
}
```

If you're using attributes to define the casting of your properties or if you don't have any casting for the properties,
you can use the `EmptyCasts` trait to avoid having to define the `casts()` method.
