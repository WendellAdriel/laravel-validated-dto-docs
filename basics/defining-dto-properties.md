# Defining DTO Properties

You can define typed properties in your `DTO` outside the constructor:

```php
class UserDTO extends ValidatedDTO
{
    public string $name;

    public string $email;

    public string $password;
}
```

Remind that the property types must be compatible with the **Cast Type** you define for them.
