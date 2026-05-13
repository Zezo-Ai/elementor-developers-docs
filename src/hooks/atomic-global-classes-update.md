# Atomic Global Classes Update

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor fires this hook after every mutation of the global classes set, allowing developers to react to changes such as additions, deletions, or reordering of global classes.

## Hook Details

* **Hook Type:** Action Hook
* **Hook Name:** `elementor/global_classes/update`
* **Affects:** Global Classes

## Hook Arguments

| Argument  | Type       | Description                                                                                              |
|-----------|------------|----------------------------------------------------------------------------------------------------------|
| `context` | _`string`_ | The rendering context — `'frontend'` or `'preview'`.                                                     |
| `changes` | _`array`_  | An associative array: `[ 'added' => string[], 'deleted' => string[], 'modified' => string[], 'order' => bool ]`. |

## Example

Invalidate a custom CSS cache whenever a global class is deleted:

```php
function my_plugin_on_global_classes_update( $context, $changes ) {
	foreach ( $changes['deleted'] as $class_id ) {
		my_plugin_drop_cached_css( $class_id );
	}
}
add_action( 'elementor/global_classes/update', 'my_plugin_on_global_classes_update', 10, 2 );
```

## Notes

Register with `accepted_args = 2` to receive both parameters.
