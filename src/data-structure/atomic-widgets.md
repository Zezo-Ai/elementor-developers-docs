# Atomic Widgets

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Atomic widgets are content elements in Elementor’s atomic architecture. Each widget is stored as an object with `elType` set to `widget` and a `widgetType` that identifies the widget (for example `e-heading`, `e-paragraph`, or `e-button`). Alongside identity and versioning, the object holds interactions, editor metadata, control values in `settings`, and optional nested elements in `elements`.

## JSON Structure

Atomic widget structure:

```json
{
	"id": "12345678",
	"version": "0.0",
	"elType": "widget",
	"widgetType": "e-heading",
	"isInner": false,
	"settings": [],
	"editor_settings": [],
	"interactions": [],
	"styles": [],
	"elements": []
}
```

## JSON Values

| Argument          | Type                 | Description |
|-------------------|----------------------|-------------|
| `id`              | _`string`_           | The unique identification key representing the element. |
| `version`         | _`string`_           | The widget schema version, used for data migrations. |
| `elType`          | _`string`_           | Always `widget` for atomic widgets. |
| `widgetType`      | _`string`_           | The widget type (for example `e-heading`, `e-paragraph`, `e-button`). |
| `isInner`         | _`boolean`_          | Whether the element is an inner element. |
| `settings`        | _`array`_/_`object`_ | Control values from the panel. Empty `array` when undefined; otherwise an `object` whose keys are control IDs. Values are usually **typed** (see below). |
| `editor_settings` | _`array`_/_`object`_ | Editor-only metadata. Not rendered on the frontend. |
| `interactions`    | _`array`_            | Interactions attached to the widget. Empty when none are defined. |
| `elements`        | _`array`_            | Nested elements. Often empty; widgets that support nesting store child elements here. |

## Typed settings

Atomic widget controls serialize as typed `{ $$type, value }` objects (see [atomic prop values](./atomic-prop-values.md)). Examples include plain strings, rich text (`html-v3`), links, and dynamic/query references, depending on the widget schema.

## Nested elements

Widgets that support nesting store children in `elements`, the same pattern as [layout atomic elements](./atomic-elements.md). Leaf widgets typically use an empty `elements` array.

## Example

A page with an `e-div-block` containing three atomic widgets (heading, paragraph, button). Paragraph text is shortened for readability; all attributes are preserved.

```json
{
	"title": "test widgets",
	"type": "page",
	"version": "0.4",
	"page_settings": [],
	"content": [
		{
			"id": "710c74bb",
			"version": "0.0",
			"elType": "e-div-block",
			"isInner": false,
			"settings": [],
			"editor_settings": [],
			"interactions": [],
			"styles": [],
			"elements": [
				{
					"id": "662f0d0d",
					"version": "0.0",
					"elType": "widget",
					"widgetType": "e-heading",
					"isInner": false,
					"settings": {
						"tag": {
							"$$type": "string",
							"value": "h3"
						},
						"title": {
							"$$type": "html-v3",
							"value": {
								"content": {
									"$$type": "string",
									"value": "My title"
								},
								"children": []
							}
						},
						"link": {
							"$$type": "link",
							"value": []
						}
					},
					"editor_settings": [],
					"interactions": [],
					"styles": [],
					"elements": []
				},
				{
					"id": "71022738",
					"version": "0.0",
					"elType": "widget",
					"widgetType": "e-paragraph",
					"isInner": false,
					"settings": {
						"paragraph": {
							"$$type": "html-v3",
							"value": {
								"content": {
									"$$type": "string",
									"value": "Lorem ipsum dolor sit amet."
								},
								"children": []
							}
						},
						"link": {
							"$$type": "link",
							"value": []
						}
					},
					"editor_settings": [],
					"interactions": [],
					"styles": [],
					"elements": []
				},
				{
					"id": "480c5582",
					"version": "0.0",
					"elType": "widget",
					"widgetType": "e-button",
					"isInner": false,
					"settings": {
						"link": {
							"$$type": "link",
							"value": {
								"destination": {
									"$$type": "query",
									"value": {
										"id": {
											"$$type": "number",
											"value": 33514
										},
										"label": {
											"$$type": "string",
											"value": "About Us"
										}
									}
								}
							}
						}
					},
					"editor_settings": [],
					"interactions": [],
					"styles": [],
					"elements": []
				}
			]
		}
	]
}
```
