# Responsive Data

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor allows users to set different values for different devices and screen sizes using [responsive controls](./../editor-controls/responsive-control/). When a user sets responsive values, Elementor stores a separate value for each device alongside the default (desktop) value in the same `settings` object.

## JSON Structure

A responsive value is saved as multiple keys in the `settings` object. The base key holds the default (desktop) value, and additional device-specific keys are created by appending the device name as a suffix:

```json
{
	"settings": {
		"control_name": "desktop value",
		"control_name_tablet": "tablet value",
		"control_name_mobile": "mobile value"
	}
}
```

If the user only sets a value for a specific device, only that device key is stored. The other devices inherit the default (desktop) value at runtime.

## Device Suffixes

Elementor supports the following default device suffixes:

| Suffix             | Device              |
|--------------------|---------------------|
| _(none)_           | Desktop (default).  |
| `_tablet`          | Tablet.             |
| `_mobile`          | Mobile.             |

Additional breakpoints introduced by the user (such as `widescreen`, `laptop`, `tablet_extra`, `mobile_extra`) follow the same pattern (`control_name_widescreen`, `control_name_laptop`, etc.).

## Examples

### Responsive Text Alignment

A widget with a text alignment control where the user has set a different alignment for each device:

```json
{
	"id": "6a637978",
	"elType": "widget",
	"widgetType": "heading",
	"isInner": false,
	"settings": {
		"title": "Add Your Heading Text Here",
		"align": "start",
		"align_tablet": "center",
		"align_mobile": "end"
	},
	"elements": []
}
```

### Responsive Spacing

A widget where a slider control sets a different spacing value per device:

```json
{
	"id": "687dba89",
	"elType": "widget",
	"widgetType": "image",
	"isInner": false,
	"settings": {
		"space_between": {
			"unit": "px",
			"size": 30,
			"sizes": []
		},
		"space_between_tablet": {
			"unit": "px",
			"size": 20,
			"sizes": []
		},
		"space_between_mobile": {
			"unit": "px",
			"size": 10,
			"sizes": []
		}
	},
	"elements": []
}
```

### Responsive Padding

A container element with different padding values for desktop, tablet and mobile:

```json
{
	"id": "458aabdc",
	"elType": "container",
	"isInner": false,
	"settings": {
		"padding": {
			"unit": "px",
			"top": "40",
			"right": "40",
			"bottom": "40",
			"left": "40",
			"isLinked": true
		},
		"padding_tablet": {
			"unit": "px",
			"top": "20",
			"right": "20",
			"bottom": "20",
			"left": "20",
			"isLinked": true
		},
		"padding_mobile": {
			"unit": "px",
			"top": "10",
			"right": "10",
			"bottom": "10",
			"left": "10",
			"isLinked": true
		}
	},
	"elements": []
}
```

### Partial Responsive Values

When the user only sets a value for one specific device, only that device key is stored:

```json
{
	"id": "6f58bb5",
	"elType": "widget",
	"widgetType": "button",
	"isInner": false,
	"settings": {
		"text": "Click Me",
		"align_mobile": "center"
	},
	"elements": []
}
```
