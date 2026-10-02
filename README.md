# Grid Avoid Doublets (WordPress-Plugin)

Grid Avoid Doublets provides an API that keeps the same post from appearing twice across
the list boxes of a [Grid](https://wordpress.org/plugins/grid/) landing page. It is
available on [WordPress.org](https://wordpress.org/plugins/grid-avoid-doublets/).

## Why

A landing page built with Grid often stacks several list boxes. Without coordination the
same post can be pulled into more than one of them. This plugin records which post IDs
have already been placed and excludes them from the query of later list boxes.

## How it works

The plugin hooks Grid's `grid_posts_box_query_args` filter and adds the already-placed
post IDs to `post__not_in`. Themes and boxes register placements through the public API
functions in `public/public-functions.php`:

| Function | Purpose |
|---|---|
| `grid_avoid_doublets_add( $content_id, $area_id )` | mark a post as placed |
| `grid_avoid_doublets_is_placed( $content_id, $area_id )` | has it been placed? |
| `grid_avoid_doublets_get_placed( $area_id )` | the placed IDs |

## Requirements

The [Grid](https://wordpress.org/plugins/grid/) plugin must be installed and active.

## Repository layout

`public/` is exactly what ships to wordpress.org; everything else is repository-only.
`plugin.php` in the root is a development wrapper that loads `public/`.

The main file `public/grid_avoid_doublets.php` must keep its name — WordPress identifies
an installed plugin by `<directory>/<main file>` and renaming it deactivates the plugin
on every site at the next update.

Releases are cut by release-please and deployed to the wordpress.org SVN by GitHub
Actions — see [.github/WORKFLOWS.md](.github/WORKFLOWS.md).

## License

GPL-3.0-or-later, see [LICENSE](LICENSE).
