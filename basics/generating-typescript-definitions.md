# Generating TypeScript Definitions

### Step 1:

Install the `spatie/typescript-transformer` package.

```bash
composer require spatie/typescript-transformer
```

### Step 2:

Publish the `typescript-transformer` config.

```bash
php artisan vendor:publish --provider="Spatie\LaravelTypeScriptTransformer\TypeScriptTransformerServiceProvider"
```

### Step 3:

Register the packages `TypeScriptCollector` and `TypeScriptTransformer` in the `typescript-transformer` config.

```php
//config/typescript-transformer.php
   ...
    /*
     * Collectors will search for classes in the `auto_discover_types` paths and choose the correct
     * transformer to transform them. By default, we include a DefaultCollector which will search
     * for @typescript annotated and #[TypeScript] attributed classes to transform.
     */

    'collectors' => [
        Spatie\TypeScriptTransformer\Collectors\DefaultCollector::class,
        Spatie\TypeScriptTransformer\Collectors\EnumCollector::class,
+       WendellAdriel\ValidatedDTO\Support\TypeScriptCollector,
    ],

    /*
     * Transformers take PHP classes(e.g., enums) as an input and will output
     * a TypeScript representation of the PHP class.
     */

    'transformers' => [
        Spatie\LaravelTypeScriptTransformer\Transformers\SpatieStateTransformer::class,
        Spatie\TypeScriptTransformer\Transformers\EnumTransformer::class,
        Spatie\TypeScriptTransformer\Transformers\SpatieEnumTransformer::class,
        Spatie\LaravelTypeScriptTransformer\Transformers\DtoTransformer::class,
+       WendellAdriel\ValidatedDTO\Support\TypeScriptTransformer,
    ],
   ...
```

### Step 4:

Run the command to generate the TypeScript types.

```bash
 php artisan typescript:transform
```

By default, the definitions are added here: `resources/types/generated.d.ts`.
