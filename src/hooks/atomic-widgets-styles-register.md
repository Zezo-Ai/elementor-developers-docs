# Atomic Widgets Styles Register

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Elementor fires this hook during style registration, allowing developers to register custom style sources into the `Atomic_Styles_Manager`.

## Hook Details

* **Hook Type:** Action Hook
* **Hook Name:** `elementor/atomic-widgets/styles/register`
* **Affects:** Styles

## Hook Arguments

| Argument   | Type                                  | Description                             |
|------------|---------------------------------------|-----------------------------------------|
| `manager`  | _`\Elementor\Modules\AtomicWidgets\Styles\Atomic_Styles_Manager`_ | The styles manager instance. |
| `post_ids` | _`array`_                             | An array of post IDs being processed.   |

## Example

```php
function my_plugin_register_atomic_style_sources( $manager, $post_ids ) {
	foreach ( $post_ids as $post_id ) {
		$manager->register_source( 'my_custom_key', $post_id, 'frontend' );
	}
}
add_action( 'elementor/atomic-widgets/styles/register', 'my_plugin_register_atomic_style_sources', 10, 2 );
```

## Notes

Register with `accepted_args = 2`. Use a `[ <your_key>, $post_id, $context ]` tuple per document.
