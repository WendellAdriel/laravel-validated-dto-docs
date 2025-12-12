# Lazy Validation

If you want your **DTO** to have validation, but not to validate while creating the **DTO**, you can set your **ValidatedDTO** to use the **Lazy Validation** feature.

```php
class LazyDTO extends ValidatedDTO
{
    public bool $lazyValidation = true;
}
```

When you set the `$lazyValidation` as `true`, you can instantiate your **DTO** without setting any attributes. When setting attributes on your **DTO**, it won't cast them automatically, the attributes will be cast only when you validate the **DTO** data by calling the `validate()` method.

```php
$dto = new LazyDTO();
$dto->name = 'John Doe';
$dto->validate(); // This is where the data is validated and the attributes are cast
```

If the validation passes, the attributes will be cast in the DTO object.

If the validation fails, it will throw a `Illuminate\Validation\ValidationException`.

This is a useful feature when using **ValidatedDTOs** with **Livewire.**

```php
use Livewire\Wireable as LivewireWireable;
use WendellAdriel\ValidatedDTO\Concerns\Wireable;

class MyDTO extends ValidatedDTO implements LivewireWireable
{
    use Wireable;
    
    public bool $lazyValidation = true;
}
```

#### The `Lazy` attribute

As an alternative, instead of setting the `$lazyValidation` as `true` in your DTO class, you can add the `Lazy` attribute to it, it will work the same way as described above.

```php
#[Lazy]
class UserDTO extends ValidatedDTO
{
    // DTO definition here
}
```
