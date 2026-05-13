# Atomic Elements

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Atomic elements are the new generation of layout elements introduced as part of Elementor's atomic architecture. Like containers, they are layout elements with nested capabilities, meaning that they can hold other elements. Each atomic element object contains information like the element id, element type, version, styling settings, interactions, editor settings and all the elements inside it.

## JSON Structure

Atomic element structure:

```json
{
	"id": "12345678",
	"version": "0.0",
	"elType": "e-div-block",
	"isInner": false,
	"interactions": [],
	"settings": [],
	"editor_settings": [],
	"styles": [],
	"elements": []
}
```

## JSON Values

| Argument          | Type                 | Description |
|-------------------|----------------------|-------------|
| `id`              | _`string`_           | The unique identification key representing the element. |
| `version`         | _`string`_           | The element schema version, used for data migrations. |
| `elType`          | _`string`_           | The element type. Such as `e-div-block`, `e-flexbox`, or `e-grid`. |
| `isInner`         | _`boolean`_          | Whether the element is an inner element. |
| `settings`        | _`array`_/_`object`_ | The element data  holding the values from the editor controls. It's an empty `array` if settings are not defined, or an `object` if the element has settings. |
| `editor_settings` | _`array`_/_`object`_ | Editor-only metadata used by the Elementor editor (for example, the element label). Not rendered on the frontend. |
| `interactions`    | _`array`_            | A list of interactions (such as event-driven behaviors) attached to the element. |
| `styles`          | _`array`_/_`object`_ | Local style definitions attached to the element, including responsive variants and pseudo-state styles. |
| `elements`        | _`array`_            | An array of objects that holds all the nested elements. |

## Nested Elements

By design, atomic elements can hold nested elements. All the inner elements are stored in the `elements` value, and they can have their own nested elements. Atomic layout elements can be freely nested within each other – for example, an `e-div-block` can contain an `e-grid`, which in turn can contain an `e-flexbox`.

## Examples

### A Page with an Atomic Div Block

An example of a page that has a single empty atomic div block:

```json
{
	"title": "Sample Page",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "6edaa5b1",
			"version": "0.0",
			"elType": "e-div-block",
			"isInner": false,
			"settings": [],
			"editor_settings": [],
			"interactions": [],
			"styles": [],
			"elements": []
		}
	]
}
```

### A Page with Nested Atomic Elements

An example of a page that has an atomic div block containing an atomic grid, which in turn contains an atomic flexbox:

```json
{
	"title": "atomic test",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "6edaa5b1",
			"version": "0.0",
			"elType": "e-div-block",
			"isInner": false,
			"settings": [],
			"editor_settings": [],
			"interactions": [],
			"styles": [],
			"elements": [
				{
					"id": "3e443808",
					"version": "0.0",
					"elType": "e-grid",
					"isInner": false,
					"settings": [],
					"editor_settings": [],
					"interactions": [],
					"styles": [],
					"elements": [
						{
							"id": "6c95f17f",
							"version": "0.0",
							"elType": "e-flexbox",
							"isInner": false,
							"settings": [],
							"editor_settings": [],
							"interactions": [],
							"styles": [],
							"elements": []
						}
					]
				}
			]
		}
	]
}
```
