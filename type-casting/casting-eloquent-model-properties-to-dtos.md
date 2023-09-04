# Casting Eloquent Model properties to DTOs

You can easily cast any **Eloquent Model** properties to your **DTOs**:

```php
class MyModel extends Model
{
    protected $fillable = ['name', 'metadata'];

    protected $casts = [
        'metadata' => AttributesDTO::class,
    ];
}
```

The **DTO** class:

```php
class AttributesDTO extends ValidatedDTO
{
    public int $age;

    public string $doc;

    protected function rules(): array
    {
        return [
            'age' => ['required', 'integer'],
            'doc' => ['required', 'string'],
        ];
    }

    protected function defaults(): array
    {
        return [];
    }

    protected function casts(): array
    {
        return [
            'age' => new IntegerCast(),
            'doc' => new StringCast(),
        ];
    }
}
```
