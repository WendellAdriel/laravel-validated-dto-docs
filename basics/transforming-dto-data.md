# Transforming DTO Data

You can convert your DTO to some formats:

### To array

```php
$dto = new UserDTO([
    'name' => 'John Doe',
    'email' => 'john.doe@example.com',
    'password' => 's3CreT!@1a2B',
]);

$dto->toArray();
// [
//     "name" => "John Doe",
//     "email" => "john.doe@example.com",
//     "password" => "s3CreT!@1a2B",
// ]
```

### To JSON string

```php
$dto = new UserDTO([
    'name' => 'John Doe',
    'email' => 'john.doe@example.com',
    'password' => 's3CreT!@1a2B',
]);

$dto->toJson();
// '{"name":"John Doe","email":"john.doe@example.com","password":"s3CreT!@1a2B"}'

$dto->toPrettyJson(); // OR LIKE THIS
// {
//     "name": "John Doe",
//     "email": "john.doe@example.com",
//     "password": "s3CreT!@1a2B"
// }
```

### To Eloquent Model

```php
$dto = new UserDTO([
    'name' => 'John Doe',
    'email' => 'john.doe@example.com',
    'password' => 's3CreT!@1a2B',
]);

$dto->toModel(\App\Models\User::class);
// App\Models\User {#3776
//     name: "John Doe",
//     email: "john.doe@example.com",
//     password: "s3CreT!@1a2B",
// }
```

## Transforming Nested Data

Be aware that when transforming the DTO, all the properties are also going to be transformed:

`Scalar Data Type` and `Array` properties will **preserve their values**.

`stdClass` properties will be transformed into arrays using **type casting**.

`UnitEnum` properties are going to be transformed into the **case name**.

`BackedEnum` properties are going to be transformed into the **case value**.

`Carbon` and `CarbonImmutable` properties are going to be transformed into strings using the `->toISOString()` method.

`Collection`, `Model` and `DTO` properties will have their nested data transformed using the same logic as above.
