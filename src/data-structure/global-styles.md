# Global Styles

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Elementor end-users can define a site-wide design system from the [site settings panel](./../editor/site-settings-panel/), including [global colors and global fonts](./../editor-controls/global-style/). When a control inherits a global value, the element's `settings` does not store the actual color or typography value. Instead, it stores a reference to the global style.

## Where Global Styles Are Stored

Global styles are not stored inside individual pages. They are saved as part of the active Elementor "Kit", which is a special WordPress post that holds the site's design system. Each global color and global font has a unique ID that pages reference.

When a page is exported, the kit data is exported alongside the page content so that global references resolve correctly on import.

## Global Reference Format

When a control uses a global value, the saved value is a special string referencing the global style by type and ID:

```
globals/<type>?id=<global-id>
```

| Part          | Description |
|---------------|-------------|
| `<type>`      | The global type. Common values are `colors` and `typography`. |
| `<global-id>` | The unique ID of the global style as defined in the site's kit. Built-in IDs include `primary`, `secondary`, `text`, `accent`. Custom globals get a generated ID. |

## JSON Structure

A global reference is saved inside the element's `settings` object using the `__globals__` key. The `__globals__` key is itself an object whose keys are control names and whose values are the global reference strings:

```json
{
	"settings": {
		"__globals__": {
			"control_name": "globals/colors?id=primary",
			"control_name": "globals/typography?id=secondary"
		}
	}
}
```

The original control key (for example `title_color`) may still appear with an empty or fallback value, but at render time Elementor resolves the value from `__globals__` and the kit.

## Examples

### Heading with a Global Color

A heading widget where the title color is inherited from the kit's primary global color:

```json
{
	"id": "6a637978",
	"elType": "widget",
	"widgetType": "heading",
	"isInner": false,
	"settings": {
		"title": "Add Your Heading Text Here",
		"__globals__": {
			"title_color": "globals/colors?id=primary"
		}
	},
	"elements": []
}
```

### Heading with Global Color and Global Typography

A heading widget where both the color and the typography are inherited from the site's design system:

```json
{
	"id": "687dba89",
	"elType": "widget",
	"widgetType": "heading",
	"isInner": false,
	"settings": {
		"title": "Add Your Heading Text Here",
		"__globals__": {
			"title_color": "globals/colors?id=secondary",
			"typography_typography": "globals/typography?id=primary"
		}
	},
	"elements": []
}
```

### Mixed Custom and Global Values

An element can mix custom values and global references. Here the title color is global, but the background color is a custom value:

```json
{
	"id": "458aabdc",
	"elType": "container",
	"isInner": false,
	"settings": {
		"background_background": "classic",
		"background_color": "#FFFFFF",
		"__globals__": {
			"heading_color": "globals/colors?id=accent"
		}
	},
	"elements": []
}
```

### Custom Global Color

Custom globals defined by the user in the site settings panel use a generated ID instead of one of the four built-in IDs:

```json
{
	"id": "6f58bb5",
	"elType": "widget",
	"widgetType": "button",
	"isInner": false,
	"settings": {
		"text": "Click Me",
		"__globals__": {
			"button_text_color": "globals/colors?id=8e2c1a4"
		}
	},
	"elements": []
}
```
