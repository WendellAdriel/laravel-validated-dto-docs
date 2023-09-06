# Custom Exceptions

You can define custom `Exceptions` by implementing the `failedValidation` method:

```php
protected function failedValidation(): void
{
    throw new ValidationException($this->validator);
}
```
