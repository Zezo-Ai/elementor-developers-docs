# Repeaters

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Some Elementor widgets and elements use the [repeater control](./../editor-controls/control-repeater/) to allow users to add repeatable blocks of fields. The repeater data is saved inside the element's `settings` object as an `array` of objects, where each object represents a single repeater item with its inner field values.

## JSON Structure

A repeater value is saved as an array of objects. Each item is an object of key-value pairs representing the inner field values. Elementor automatically adds a unique `_id` to every item:

```json
{
	"settings": {
		"repeater_control_name": [
			{
				"_id": "abcd1234",
				"field_name": "field value",
				"field_name": "field value"
			},
			{
				"_id": "efgh5678",
				"field_name": "field value",
				"field_name": "field value"
			}
		]
	}
}
```

## JSON Values

Each repeater item contains the following:

| Argument      | Type       | Description |
|---------------|------------|-------------|
| `_id`         | _`string`_ | A unique identifier automatically generated for the repeater item. Used as a CSS selector reference (`elementor-repeater-item-{{_id}}`) and to track the item when editing. |
| _field name_  | _`mixed`_  | One key per inner field defined in the repeater control. The value type depends on the inner control type (string, object, array, etc.). |

## Examples

### Simple Repeater

A widget with a repeater that holds a list of items, where each item has a title and a text content:

```json
{
	"id": "6a637978",
	"elType": "widget",
	"widgetType": "test-widget",
	"isInner": false,
	"settings": {
		"list": [
			{
				"_id": "a1b2c3d",
				"list_title": "Title #1",
				"list_content": "Item content. Click the edit button to change this text."
			},
			{
				"_id": "e4f5g6h",
				"list_title": "Title #2",
				"list_content": "Item content. Click the edit button to change this text."
			}
		]
	},
	"elements": []
}
```

### Repeater with Mixed Field Types

A repeater where each item contains a text field, a URL field and a color field:

```json
{
	"id": "687dba89",
	"elType": "widget",
	"widgetType": "test-widget",
	"isInner": false,
	"settings": {
		"list": [
			{
				"_id": "1a2b3c4",
				"text": "List Item #1",
				"link": {
					"url": "https://elementor.com/",
					"is_external": "",
					"nofollow": ""
				},
				"item_color": "#FF0000"
			},
			{
				"_id": "5d6e7f8",
				"text": "List Item #2",
				"link": {
					"url": "https://elementor.com/contact/",
					"is_external": "on",
					"nofollow": ""
				},
				"item_color": "#00FF00"
			}
		]
	},
	"elements": []
}
```

### Repeater with Responsive Fields

Repeater items can also hold [responsive values](./responsive-data/) when the inner controls are responsive. Each device suffix is added directly to the inner field name:

```json
{
	"id": "6f58bb5",
	"elType": "widget",
	"widgetType": "test-widget",
	"isInner": false,
	"settings": {
		"slides": [
			{
				"_id": "x1y2z3a",
				"slide_title": "First Slide",
				"slide_align": "start",
				"slide_align_tablet": "center",
				"slide_align_mobile": "center"
			},
			{
				"_id": "b4c5d6e",
				"slide_title": "Second Slide",
				"slide_align": "end",
				"slide_align_tablet": "center",
				"slide_align_mobile": "start"
			}
		]
	},
	"elements": []
}
```
