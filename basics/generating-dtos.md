# Generating DTOs

You can create `DTOs` using the `make:dto` command:

```
php artisan make:dto UserDTO
```

The `DTOs` are going to be created inside `app/DTOs` by default. You can customize the path by updating the namespace
property in the `config/dto.php` file:

```php
/*
|--------------------------------------------------------------------------
| NAMESPACE
|--------------------------------------------------------------------------
|
| The namespace where your DTOs will be created.
|
*/

'namespace' => 'App\\DTOs',
```

Compared to v2, the generated DTO from v3 is more simple and only contains the most used methods:

- `rules()` (For Validated DTOs only)
- `defaults()`
- `casts()`

If you want to customize further your DTO add the missing methods when needed.

- `messages()`
- `attributes()`
- `mapData()`
- `mapToTransform()`
