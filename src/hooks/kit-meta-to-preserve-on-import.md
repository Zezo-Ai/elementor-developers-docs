# Kit Meta to Preserve on Import

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor fires this filter during kit imports, allowing developers to preserve specific kit-level metadata so it is not overwritten.

## Hook Details

* **Hook Type:** Filter Hook
* **Hook Name:** `elementor/kit/meta_to_preserve_on_kit_import`
* **Affects:** Kit Import

## Hook Arguments

| Argument    | Type      | Description                                           |
|-------------|-----------|-------------------------------------------------------|
| `meta_keys` | _`array`_ | An array of meta keys that should survive a kit import. |

## Example

```php
function my_plugin_preserve_kit_meta( array $meta_keys ) {
	$meta_keys[] = 'my_plugin_kit_meta_key';
	return $meta_keys;
}
add_filter( 'elementor/kit/meta_to_preserve_on_kit_import', 'my_plugin_preserve_kit_meta' );
```

## Notes

Global Classes itself registers four keys here (order, frontend labels, preview labels, sync map).
