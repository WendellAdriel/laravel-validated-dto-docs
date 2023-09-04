# Create Your Own Type Cast

### Castable classes

You can easily create new `Castable` types for your project by implementing the `WendellAdriel\ValidatedDTO\Casting\Castable` interface. This interface has a single method that must be implemented:

```php
/**
 * Casts the given value.
 *
 * @param  string  $property
 * @param  mixed  $value
 * @return mixed
 */
public function cast(string $property, mixed $value): mixed;
```

Let's say that you have a `URLWrapper` class in your project, and you want that when passing a URL into your `DTO` it will always return a `URLWrapper` instance instead of a simple string:

```php
class URLCast implements Castable
{
    /**
     * @param  string  $property
     * @param  mixed  $value
     * @return URLWrapper
     */
    public function cast(string $property, mixed $value): URLWrapper
    {
        return new URLWrapper($value);
    }
}
```

Then you could apply this to your DTO:

```php
class CustomDTO extends ValidatedDTO
{
    protected function rules(): array
    {
        return [
            'url' => ['required', 'url'],
        ];
    }

    protected function defaults(): array
    {
        return [];
    }

    protected function casts(): array
    {
        return [
            'url' => new URLCast(),
        ];
    }
}
```

### Callable casts

You can also create new `Castable` types for your project by using a `callable/callback`:

```php
class CustomDTO extends ValidatedDTO
{
    protected function rules(): array
    {
        return [
            'url' => ['required', 'url'],
        ];
    }

    protected function defaults(): array
    {
        return [];
    }

    protected function casts(): array
    {
        return [
            'url' => function (string $property, mixed $value) {
                return new URLWrapper($value);
            },
        ];
    }
}
```
