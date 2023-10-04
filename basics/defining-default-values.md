# Defining Default Values

Sometimes we can have properties that are optional and that can have default values. You can define the default values for your `DTO` properties in the `defaults` function:

```php
class UserDTO extends ValidatedDTO
{
    protected function rules(): array
    {
        return [
            'name'     => ['required', 'string'],
            'email'    => ['required', 'email'],
            'username' => ['sometimes', 'string'],
            'password' => [
                'required',
                Password::min(8)
                    ->mixedCase()
                    ->letters()
                    ->numbers()
                    ->symbols()
                    ->uncompromised(),
            ],
        ];
    }

    protected function defaults(): array
    {
        return [
            'username' => Str::snake($this->name),
        ];
    }
}
```

With the `DTO` definition above you could run:

```php
$dto = new UserDTO([
    'name' => 'John Doe',
    'email' => 'john.doe@example.com',
    'password' => 's3CreT!@1a2B'
]);

$dto->username; // 'john_doe'
```

Alternatively, for simpler cases, you can use the `DefaultValue` attribute:

```php
use WendellAdriel\ValidatedDTO\Attributes\DefaultValue;
use WendellAdriel\ValidatedDTO\Concerns\EmptyDefaults;

class UserDTO extends ValidatedDTO
{
    use EmptyDefaults;

    public string $name;

    public string $email;

    #[DefaultValue(true)]
    public bool $active;
}
```

If you're using attributes to define your properties default values or if you don't have any defaults values for the properties,
you can use the `EmptyDefaults` trait to avoid having to define the `defaults()` method.
