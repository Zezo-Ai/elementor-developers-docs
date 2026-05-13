# Atomic Global Classes

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Intermediate" />

Reads and writes use two contexts. **Frontend** is published data. **Preview** is the editor draft. Each side uses its own meta keys (`…` vs `…_preview`).

Global classes live on `e_global_class` posts. Class JSON is `_elementor_global_class_data` / `_elementor_global_class_data_preview`. Documents store usage in `_elementor_used_global_class` / `_elementor_used_global_class_preview`. Reverse indexes: `_elementor_global_class_using_documents` (+ preview). Documents may also set `_elementor_global_class_usage_indexed` flags. The active Kit stores display order, `class_id → label` maps (frontend vs preview), a design-system sync map, and `class_id → post_id` lookup.

Each item matches the [atomic style](./atomic-styles.md) shape (`id`, `label`, `type`, `variants`).

## PHP access

```php
use Elementor\Modules\GlobalClasses\Global_Classes_Repository;

$repository = Global_Classes_Repository::make();
$repository->set_preview( true );  // draft
$repository->set_preview( false ); // published (default)
```

| Method | Role |
|--------|------|
| `all_labels()` | Ordered `class_id → label` (cheap). |
| `get()`, `get_by_ids()` | One or many items; missing → `null` / omitted. |
| `get_order()` | Ordered ID list. |
| `each_item( $cb, … )` | Stream all classes in order. |
| `all( $force )` | Full `Global_Classes` — heavy. |
| `apply_changes` / `put` | Persist diffs or replace-all; both fire `elementor/global_classes/update`. |
| `update_order_and_labels` | Kit order/labels only. |
| `delete_all()` | Remove all classes in the current context. |

## REST API

Prefix every route with `/wp-json/elementor/v1/`. On **GET**, optional `context`: `frontend` (default) or `preview`.

| Method | Suffix | Notes |
|--------|--------|-------|
| `GET`  | `global-classes` | Labels only, in order. |
| `GET`  | `global-classes/post` | Query: `post_id`. Full items for that document. |
| `GET`  | `global-classes/styles` | Query: `ids` (comma-separated). Bulk by ID. |
| `GET`  | `global-classes/usage` | Site-wide usage; `manage_options`. |
| `PUT`  | `global-classes` | Body: `changes`, `items`, `order`; optional `context`. Update-class capability. |

**`PUT` body (minimal):** `changes` = `{ added, deleted, modified, order? }`. `items` = only touched classes, `class_id` → full item. `order` = full ID list after the op. Set `changes.order: true` when reordering so caches invalidate. Hard cap: **1000** classes.