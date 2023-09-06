# Changelog

Here's a quick overview of the new features in the latest major versions of the package.

## 3.0.0

- Use **DTO** as it was a **Form Request**
- Ability to customize the path/namespace of the generated DTOs
- DTO classes generated with the make command are more slim
- Ability to cast array items when using the `ArrayCast`
- New `EnumCast` for casting values to Enums. Work with `UnitEnum` and `BackedEnum`
- `mapBeforeValidation()` was renamed to `mapData()`
- `mapBeforeExport()` was renamed to `mapToTransform()`
- `->toJson()` method now returns a JSON string without any formatting. Use `->toPrettyJson()` instead
