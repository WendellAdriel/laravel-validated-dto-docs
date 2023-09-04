# Wireable DTOs

If you're using [**Laravel Livewire**](https://laravel-livewire.com/), you can turn your DTOs into **wireable** DTOs by adding the `WendellAdriel\ValidatedDTO\Concerns\Wireable` trait to your DTOs:

```php
class UserDTO extends ValidatedDTO
{
    use Wireable;
    // Your DTO code...
}
```
