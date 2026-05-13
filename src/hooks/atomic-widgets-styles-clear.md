# Atomic Widgets Styles Clear

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor fires this hook when style caches should be invalidated. The `$key` argument is a hierarchical tuple that indicates the scope of the invalidation.

## Hook Details

* **Hook Type:** Action Hook
* **Hook Name:** `elementor/atomic-widgets/styles/clear`
* **Affects:** Styles

## Hook Arguments

| Argument | Type      | Description                                       |
|----------|-----------|---------------------------------------------------|
| `key`    | _`array`_ | A hierarchical tuple describing the clear scope.  |

### Key Reference

| Key                              | Meaning                              |
|----------------------------------|--------------------------------------|
| `[ 'global' ]`                   | Full clear, all documents and contexts. |
| `[ 'global', $context ]`         | One context, all documents.          |
| `[ 'global', $post_id ]`         | One document, both contexts.         |
| `[ 'global', $post_id, $context ]` | One document and context.          |

## Example

```php
function my_plugin_clear_atomic_styles_cache( array $key ) {
	if ( ( $key[0] ?? null ) !== 'global' ) {
		return;
	}
	my_plugin_clear_global_cache( $key );
}
add_action( 'elementor/atomic-widgets/styles/clear', 'my_plugin_clear_atomic_styles_cache' );
```
