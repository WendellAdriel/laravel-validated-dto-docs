# Resource DTOs

If you want to use DTOs to wrap, type and transform your API responses, you can use the `ResourceDTO` class. This class will have the same features as the `SimpleDTO` class and will implement the `Illuminate\Contracts\Support\Responsable` interface:

```php
class UserResourceDTO extends ResourceDTO
{
    public string $name;
    public string $email;
    public int $age;
    // Your DTO methods...
}
```

Then you can return your DTOs from your controllers:

```php
class UserController extends Controller
{
    public function show(int $id)
    {
        return UserResourceDTO::fromModel(User::findOrFail($id));
    }
}
```

You can also return a collection/list of your DTOs as a response using the `ResourceDTO::collection()` method:

```php
class UserController extends Controller
{
    public function index()
    {
        return UserResourceDTO::collection(User::all());
    }
}
```

This way every item in the collection will be converted to a `UserResourceDTO` instance before sending the response to the client, using all the typing, casting and mapping features of your DTO class.

To generate a `ResourceDTO` you can use the `--resource` flag:

```bash
php artisan make:dto UserResourceDTO --resource
```
