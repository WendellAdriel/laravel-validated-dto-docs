# Changelog

Here's a quick overview of the new features in the latest major versions of the package.

## 4.1.0

* Added feature for generating TypeScript definitions from DTOs.

## 4.0.0

* Added support for Laravel 12.
* Removed support for Laravel 9 and 10.
* Removed support for PHP 8.1, minimum version now is 8.2.

## 3.10.0

* Added Lazy Validation feature.

## 3.9.0

* Renamed the `$data` property to `$dtoData` and marked it as `internal` to avoid issues with conflicts.

## 3.8.0

* Added support for Arrayable.

## 3.7.0

* The `buildDataForExport` method is now protected, making it possible to create custom Data Transformer methods for the DTOs.

## 3.6.0

* The `$data` property resets to an empty array after the DTO is initialized.

## 3.5.0

* Laravel 11 support.

## 3.4.0

* Added the `dto:stubs` command to publish the DTO stubs to be customized.
* Fixed issue with file validation.

## 3.3.0

* Added the `after` method to `ValidatedDTO` to be able to use the **After Hook** when validating data.

## 3.2.0

* Added the `Cast` attribute to define custom casting for DTO properties.

## 3.1.0

* Added the `Rules` attribute to define custom validation rules for DTO properties.
* Added the `DefaultValue` attribute to define default values for DTO properties.
* Added the `Map` attribute to define the custom mapping for DTO properties.
* Added the `EmptyCasts` trait to be used by DTOs that don't have any casts.
* Added the `EmptyRules` trait to be used by DTOs that don't have any validation rules or that are using the `Rules` attribute for validation.
* Added the `EmptyDefaults` trait to be used by DTOs that don't have any default values or that are using the `DefaultValue` attribute for default values.

## 3.0.0

* Use **DTO** as it was a **Form Request**
* Ability to customize the path/namespace of the generated DTOs.
* DTO classes generated with the make command are slimmer.
* Ability to cast array items when using the `ArrayCast`.
* New `EnumCast` for casting values to Enums. Work with `UnitEnum` and `BackedEnum`.
* `mapBeforeValidation()` was renamed to `mapData()`.
* `mapBeforeExport()` was renamed to `mapToTransform()`.
* `->toJson()` method now returns a JSON string without any formatting. Use `->toPrettyJson()` instead.
