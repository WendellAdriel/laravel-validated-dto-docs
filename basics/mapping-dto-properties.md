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

#### **Mapping nested data to flat data**

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

#### **Mapping nested data to flat data**

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
