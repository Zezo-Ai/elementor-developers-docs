# Atomic Prop Values

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Advanced" />

Atomic controls often save values as a small object: a `$$type` string plus a `value` payload. The props resolver uses `$$type` to match the schema (and union members), to recurse into nested object/array props, and to pick the **transformer** that receives `value` (after nested resolution) and returns frontend-ready data. An optional `disabled` flag is passed through on the transform context.

## JSON Structure

```json
{
	"$$type": "string",
	"value": "Hello"
}
```

## JSON Values

| Argument | Type       | Description |
|----------|------------|-------------|
| `$$type` | _`string`_ | Prop kind / transformer key; must match the prop type for that control (and selects the branch for union types). |
| `value`  | _varies_   | Input passed to the transformer for that `$$type`; may contain further `{ $$type, value }` objects when the prop is composite. |

Allowed `$$type` values and the exact shape of `value` come from each widget’s schema in code. See [atomic widgets](./atomic-widgets.md) for how `settings` use these objects, and [atomic styles](./atomic-styles.md) for the same pattern inside style `variants[].props`.

## Examples by structure

The snippets below are trimmed from real document data. They highlight **shape**: whether `value` is a scalar, a sparse object, a nested tree of typed nodes, a homogeneous map, or a typed array—regardless of which widget or control produced them. Resolution still walks every nested `{ "$$type", "value" }` until the tree is plain JSON (strings, numbers, booleans, or `null`). Concrete `$$type` strings always come from the control schema in code.

### Composite object (mixed typed fields and plain data)

`value` is an object where **named keys** carry further typed props, plain arrays, or literals. One branch might be a full `{ "$$type", "value" }` while another stays a raw array or string.

```json
{
	"$$type": "html-v3",
	"value": {
		"content": {
			"$$type": "string",
			"value": "My title"
		}
	}
}
```


### Deep nesting (typed object inside typed object)

The same sparse shell can grow a **chain** of wrappers: a key inside `value` is itself a typed object whose own `value` contains more typed leaves (here, internal targets resolved as id + label).

```json
{
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
		},
		"isTargetBlank": null
	}
}
```

### Typed array of primitives

`value` is an array at the top level; elements are **not** wrapped again unless the schema says so. Typical case: a list of stable ids referenced elsewhere (for example keys under `styles` on the element).

```json
{
	"$$type": "classes",
	"value": ["e-132b96e-91b05d4"]
}
```

### Composite object with a single nested typed subtree

A flat-looking object whose fields are mostly **one** nested typed prop (plus room for more keys in other saves).

```json
{
	"$$type": "background",
	"value": {
		"color": {
			"$$type": "color",
			"value": "#e8e8e8"
		}
	}
}
```

### Homogeneous map (same inner shape per key)

`value` behaves like a **record**: several keys share the same structural pattern (here every side resolves through the same `size` shape).

```json
{
	"$$type": "dimensions",
	"value": {
		"block-start": {
			"$$type": "size",
			"value": {
				"unit": "px",
				"size": 15
			}
		},
		"block-end": {
			"$$type": "size",
			"value": {
				"unit": "px",
				"size": 15
			}
		},
		"inline-start": {
			"$$type": "size",
			"value": {
				"unit": "px",
				"size": 5
			}
		},
		"inline-end": {
			"$$type": "size",
			"value": {
				"unit": "px",
				"size": 5
			}
		}
	}
}
```

### Array of composite items

`value` is an array whose **items** are full typed objects again—useful for ordered lists such as shadow layers.

```json
{
	"$$type": "box-shadow",
	"value": [
		{
			"$$type": "shadow",
			"value": {
				"hOffset": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 0
					}
				},
				"vOffset": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 0
					}
				},
				"blur": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 10
					}
				},
				"spread": {
					"$$type": "size",
					"value": {
						"unit": "px",
						"size": 0
					}
				},
				"color": {
					"$$type": "color",
					"value": "rgba(0, 0, 0, 0.75)"
				},
				"position": null
			}
		}
	]
}
```

