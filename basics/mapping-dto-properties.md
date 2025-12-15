# Mapping DTO properties

### Mapping data on instantiation

Sometimes the data you have to validate is not the same as you want in your DTO. You can use the `mapData` method to map your data when the DTO instantiation occurs:

```php
protected function mapData(): array
{
    return [
        'full_name' => 'name',
    ];
}
```

The code above will map the `full_name` property to the `name` property before the DTO instantiation. So your Request/Array/etc can have a `full_name` property and your DTO will have a `name` property instead.

Alternatively, for simpler cases, you can use the `Map` attribute, defining the `data` parameter:

```php
use WendellAdriel\ValidatedDTO\Attributes\Map;

class UserDTO extends ValidatedDTO
{
    #[Map(data: 'full_name')]
    public string $name;

    public string $email;

    public bool $active;
}
```

#### Mapping nested data to flat data

Imagine that you have a `NameDTO` like this:

```php
class NameDTO extends ValidatedDTO
{
    public string $first_name;

    public string $last_name;

    protected function rules(): array
    {
        return [
            'first_name' => ['required', 'string'],
            'last_name' => ['required', 'string'],
        ];
    }
}
```

But in your Request, the data comes like this:

```php
[
    'name' => [
        'first_name' => 'John',
        'last_name' => 'Doe',
    ],
]
```

You can add this to the `mapData` method:

```php
protected function mapData(): array
{
    return [
        'first_name' => 'name.first_name',
        'last_name' => 'name.last_name',
    ];
}
```

This way, the `first_name` and `last_name` properties will be mapped to the `name.first_name` and `name.last_name` properties of your request.

#### The `Receive` attribute

You can use the `Receive` attribute when you want to map all the incoming data in a particular character casing, for example, you may receive all the data from your UI in `snake_case`, but the properties in the DTO are in `camelCase`, so instead of mapping each property individually, you can use the `Receive` attribute:

```php
#[Receive(PropertyCase::SnakeCase)]
class UserDTO extends ValidatedDTO
{
    public string $firstName;
    public string $lastName;
}

// Accept snake_case input
$dto = new UserDTO([
    'first_name' => 'John',
    'last_name' => 'Doe'
]);
```

### Mapping data before transforming

Sometimes the data you have in your DTO is not the same you want to your Model, Array, JSON. You can use the `mapToTransform` method to map your data before transforming your DTO to another type:

```php
protected function mapToTransform(): array
{
    return [
        'name' => 'username',
    ];
}
```

The code above will map the `name` property to the `username` property before transforming your DTO to another type. So the resulting type will have a `username` property instead of a `name` property.

Alternatively, for simpler cases, you can use the `Map` attribute, defining the `transform` parameter:

```php
use WendellAdriel\ValidatedDTO\Attributes\Map;

class UserDTO extends ValidatedDTO
{
    #[Map(transform: 'username')]
    public string $name;

    public string $email;

    public bool $active;
}
```

#### Mapping nested data to flat data

Imagine that you have a `UserDTO` like this:

```php
class UserDTO extends ValidatedDTO
{
    public NameDTO $name;

    public string $email;

    protected function rules(): array
    {
        return [
            'name' => ['required', 'array'],
            'email' => ['required', 'email'],
        ];
    }
```

But your `User` model is like this:

```php
class User extends Model
{
    protected $fillable = [
        'first_name',
        'last_name',
        'email',
    ];
}
```

You can add this to the `mapToTransform` method:

```php
protected function mapToTransform(): array
{
    return [
        'name.first_name' => 'first_name',
        'name.last_name' => 'last_name',
    ];
}
```

This way, when calling the `toModel` method, the `name.first_name` and `name.last_name` properties of your DTO will be mapped to the `first_name` and `last_name` properties of your Model.

You can combine both methods to map your data before instantiation and before transformation. If you combine both examples above your request will have a `full_name` property, your DTO will have a `name` property and when transformed the result will have a `username` property.

#### The `SkipOnTransform` attribute

Sometimes you don't want to create an array, JSON or Model with all the properties from the DTO. For that, you can use the SkipOnTransform attribute.

```php
final class UserDTO extends SimpleDTO
{
    use EmptyCasts,
        EmptyDefaults,
        EmptyRules;

    #[Rules(['required', 'string'])]
    public string $name;

    #[Cast(IntegerCast::class)]
    #[SkipOnTransform]
    #[Rules(['required', 'integer'])]
    public int $age;
}
```

With the above, when calling methods like `$dto->toArray()`, the array won't have the `age` property set.

```php
$dto->toArray(); // ['name' => 'John Doe']
```

#### The `Provide` attribute

You can use the `Provide` attribute when you want to transform all the DTO data to a particular character casing, for example, you may need to connect to a 3rd-party service that accepts all the input in `PascalCase`, but the properties in the DTO are in `camelCase`, so instead of mapping each property individually, you can use the `Provide` attribute:

```php
#[Provide(PropertyCase::PascalCase)]
class UserDTO extends ValidatedDTO
{
    public string $firstName;
    public string $lastName;
}

// Provide PascalCase output
$dto->toArray();
// ['FirstName' => 'John', 'LastName' => 'Doe']
```
