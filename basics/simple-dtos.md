# Simple DTOs

If you don't need to validate the data, you can use the `SimpleDTO` class instead of the `ValidatedDTO` class. The DTOs created with this class will not validate the data, but will still have all the other features of the `ValidatedDTO` class:

```php
class SimpleUserDTO extends SimpleDTO
{
    public string $name;
    public string $email;
    public int $age;
    protected function defaults(): array
    {
        return [];
    }
    protected function casts(): array
    {
        return [
            'name' => new StringCast(),
            'email' => new StringCast(),
            'age' => new IntegerCast(),
        ];
    }
    protected function mapBeforeValidation(): array
    {
        return [
            'username' => 'name',
            'user_email' => 'email',
        ];
    }
    protected function mapBeforeExport(): array
    {
        return [
            'name' => 'customer_name',
            'email' => 'customer_email',
        ];
    }
}
```

To generate a `SimpleDTO` you can use the `--simple` flag:

```bash
php artisan make:dto SimpleUserDTO --simple
```
