# Defining Validation Rules

You can validate data in the same way you validate `Request` data:

```php
class UserDTO extends ValidatedDTO
{
    protected function rules(): array
    {
        return [
            'name'     => ['required', 'string'],
            'email'    => ['required', 'email'],
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
}
```

Alternatively, for simpler cases, you can use the `Rules` attribute:

```php
use WendellAdriel\ValidatedDTO\Attributes\Rules;
use WendellAdriel\ValidatedDTO\Concerns\EmptyRules;

class UserDTO extends ValidatedDTO
{
    use EmptyRules;

    #[Rules(['required', 'string', 'min:3', 'max:255'])]
    public string $name;

    #[Rules(rules: ['required', 'email', 'max:255'], messages: ['email.email' => 'The given email is not a valid email address.'])]
    public string $email;

    #[Rules(['sometimes', 'boolean'])]
    public bool $active;
}
```

If you're using attributes to validate your data, you can use the `EmptyRules` trait to avoid having to define the `rules()` method.
