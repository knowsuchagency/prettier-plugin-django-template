# prettier-plugin-django-template

## WARNING: This doens't work yet

Formatter plugin for Django template files.

## Install

```bash
npm install --save-dev prettier prettier-plugin-django-template
```

Add the plugin to your `.prettierrc`:
```json
{
  "plugins": ["prettier-plugin-django-template"]
}
```

## Use

To format basic .html files, you'll have to override the used parser inside your `.prettierrc`:
```json
{
  "overrides": [
    {
      "files": ["*.html"],
      "options": {
        "parser": "django-template"
      }
    }
  ]
}
```

Run it on all html files in your project:
```bash
npx prettier --write **/*.html
```

If you don't have a prettier config you can run the plugin with this command:
```bash
npx prettier --write **/*.html --plugin=prettier-plugin-django-template
```

### Ignoring Code

Using range ignores is the best way to tell prettier to ignore part of files. Most of the time this is necessary for Django tags inside `script` or `style` tags:

```html
<!-- prettier-ignore-start -->
  <script>
    window.someData = {{ data | safe }}
  </script>
<!-- prettier-ignore-end -->

<!-- prettier-ignore-start -->
  <style>
    :root { --accent-color: {{ theme_accent_color }} }
  </style>
<!-- prettier-ignore-end -->
```

## Options

This Plugin provides additional options:

### Quote Attributes

Surrounds the value of html attributes with quotes. This option was introduced to support [JinjaX](https://jinjax.scaletti.dev/) syntax.

`true` - Example:
```js
<Paginator items="{products}" />
```

`false` - Example:
```js
<Paginator items={products} />
```

| Default | CLI Override            | API Override              |
| ------- | ----------------------- | ------------------------- |
| `true`  | `--no-quote-attributes` | `quoteAttributes: <bool>` |
