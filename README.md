# Read More Extra Field

Read More Extra Field adds a **Read more** link to node displays as an extra field. Each display (a content type and view mode) can give the link its own label, classes and attributes.

## Requirements

- Drupal 10.2 or 11
- [Extra Field](https://www.drupal.org/project/extra_field) (`^2 || ^3`)
- [Extra Field Settings Provider](https://www.drupal.org/project/extra_field_plus) (`^3`)
- [Token](https://www.drupal.org/project/token) (optional): adds token support to some settings

## Installation

```bash
drush en readmore_extrafield
```

Enabling the module also enables Extra Field and Extra Field Settings Provider, which are dependencies.

## Usage

1. Go to **Structure > Content types > [content type] > Manage display**, and choose the view mode (for example Teaser).
2. Move **Read more** out of Disabled and place it where you want the link.
3. Open its settings (the cog) to change it.

The extra field is available on every node display.

| Setting | Description |
| --- | --- |
| Label | The link text. Defaults to "Read more". |
| Link classes | Extra CSS classes for the link, separated by spaces. |
| Link "title" attribute | The `title` attribute. |
| Link "rel" attribute | The `rel` attribute. |
| Link "target" attribute | The `target` attribute. |

With the Token module installed, the label, classes, and title attribute accept tokens of the node, for example `Read [node:title]`, and a token browser appears in the settings. Tokens that cannot be filled in are removed.

The link always points to the node's own page and has the class `readmore-extrafield-link`.

## Theming

The link renders through `templates/readmore-extrafield.html.twig`:

```twig
<div class="readmore-extrafield">{{ link(title, url, attributes) }}</div>
```

The template has the variables `title`, `url`, `attributes`, `entity` and `view_mode`. To override it in a theme, copy the template and use one of these suggestions in the file name, from least to most specific (view mode `teaser` and node type `article` as examples):

- `readmore-extrafield--teaser.html.twig`
- `readmore-extrafield--node.html.twig`
- `readmore-extrafield--node--teaser.html.twig`
- `readmore-extrafield--node--article.html.twig`
- `readmore-extrafield--node--article--teaser.html.twig`
- `readmore-extrafield--node--{node id}.html.twig`
- `readmore-extrafield--node--{node id}--teaser.html.twig`

## Upgrading to 3.x

Version 3 requires Extra Field and Extra Field Settings Provider. Install them before running `drush updatedb`: the module reports an error on the update page when they are missing. Update `readmore-extrafield.html.twig` if your theme overrides it, since its variables changed.

## Files

- `readmore_extrafield.info.yml`: module metadata and dependencies.
- `readmore_extrafield.module`: the `readmore_extrafield` theme hook and its template suggestions.
- `readmore_extrafield.install`: the update requirement check and the update that enables the dependencies.
- `src/Plugin/ExtraField/Display/ReadmoreExtrafield.php`: the extra field and its settings form.
- `templates/readmore-extrafield.html.twig`: the link markup.
- `config/schema/readmore_extrafield.schema.yml`: the settings schema.
- `tests/`: functional and JavaScript tests.
