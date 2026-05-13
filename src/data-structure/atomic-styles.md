# Atomic Styles

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

An atomic **style** is a reusable class definition: it has an identifier, a user-facing label, and one or more **variants**. Each variant targets a responsive breakpoint and pseudo-state (`meta`) and holds a flat map of style **props**. Prop values are usually typed objects (`$$type` + `value`); see [atomic prop values](./atomic-prop-values.md). The `id` is what ties the style to the data layer and to the generated CSS class; for some sources (for example global classes) the visible class name may follow the `label` instead.

## JSON Structure

```json
{
	"id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
	"label": "Primary button",
	"type": "class",
	"variants": [
		{
			"meta": {
				"breakpoint": "desktop",
				"state": null
			},
			"props": {
				"color": {
					"$$type": "color",
					"value": "#111111"
				}
			}
		}
	]
}
```

## JSON Values

| Argument   | Type       | Description |
|------------|------------|-------------|
| `id`       | _`string`_ | Stable id for the style (often aligned with the CSS class used in markup). |
| `label`    | _`string`_ | Name shown in the UI; may also drive the public class name depending on where the style is stored. |
| `type`     | _`string`_ | Style kind; `class` means a class-based rule (for example `.e-{id}`). |
| `variants` | _`array`_  | One object per breakpoint/state combination; each entry has `meta` and `props`. Duplicate `meta` combinations must not appear on the same style. |

## Example: breakpoints, states, and prop variety

Variants are keyed by **`meta.breakpoint`** and **`meta.state`**. Together they let one class describe a default look on desktop, a hover override on that same breakpoint, and a different default on mobile—each as its own object in `variants`. `meta.state` is usually `null` for the normal (non-pseudo) state; another entry with `state: "hover"` layers interaction styling. Props you omit in a variant are not set for that breakpoint/state pair, so narrow variants (for example hover only changing the background) stay small.

```json
{
	"id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
	"label": "Promo banner",
	"type": "class",
	"variants": [
		{
			"meta": {
				"breakpoint": "desktop",
				"state": null
			},
			"props": {
				"color": {
					"$$type": "color",
					"value": "#1a1a1a"
				},
				"background": {
					"$$type": "background",
					"value": {
						"color": {
							"$$type": "color",
							"value": "#eef6ff"
						}
					}
				},
				"padding": {
					"$$type": "dimensions",
					"value": {
						"block-start": {
							"$$type": "size",
							"value": {
								"unit": "px",
								"size": 12
							}
						},
						"block-end": {
							"$$type": "size",
							"value": {
								"unit": "px",
								"size": 12
							}
						},
						"inline-start": {
							"$$type": "size",
							"value": {
								"unit": "px",
								"size": 16
							}
						},
						"inline-end": {
							"$$type": "size",
							"value": {
								"unit": "px",
								"size": 16
							}
						}
					}
				},
				"font-size": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 16
					}
				}
			}
		},
		{
			"meta": {
				"breakpoint": "desktop",
				"state": "hover"
			},
			"props": {
				"background": {
					"$$type": "background",
					"value": {
						"color": {
							"$$type": "color",
							"value": "#dbeafe"
						}
					}
				}
			}
		},
		{
			"meta": {
				"breakpoint": "mobile",
				"state": null
			},
			"props": {
				"font-size": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 18
					}
				}
			}
		}
	]
}
```
