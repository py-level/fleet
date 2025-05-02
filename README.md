# Fleet

Fleet is a Python templating engine using Jinja2, mimicking Vue.js syntax. It uses `p-` directives (e.g., `p-if`, `p-for`) and `{{ }}` for control and interpolation, avoiding `{% %}`. Ideal for Python web projects, it enables dynamic, secure HTML rendering with a familiar client-server templating syntax. (280 characters)

## Installation

Install Fleet via pip:

```bash
pip install fleet
```

Requires `beautifulsoup4` and `jinja2`. For I18N support, install `babel`:

```bash
pip install babel
```

## Usage

1. **Create an HTML Template** (`templates/index.html`):

```html
{{ extends "base.html" }}
{{ block content }}
    <div p-if="show">
        <p p-text="message"></p>
    </div>
    <ul>
        <li p-for="item in items" p-key="item.id">{{ item.name }}</li>
    </ul>
    <p>{{ _gettext('Welcome') }}</p>
{{ endblock }}
```

2. **Base Template** (`templates/base.html`):

```html
<!DOCTYPE html>
<html>
<body>
    {{ block content }}{{ endblock }}
</body>
</html>
```

3. **Render with Python** (e.g., Flask):

```python
from flask import Flask
from fleet import render_template

app = Flask(__name__)

@app.route('/')
def index():
    with open('templates/index.html', 'r') as file:
        template = file.read()
    data = {
        'show': True,
        'message': 'Hello, World!',
        'items': [{'id': 1, 'name': 'Item 1'}, {'id': 2, 'name': 'Item 2'}]
    }
    return render_template(template, data, sandboxed=True)

if __name__ == '__main__':
    app.run(debug=True)
```

## Features

- **Vue.js-Like Syntax:** Use `p-` directives (`p-if`, `p-for`, `p-bind`, etc.) and `{{ }}` for control and interpolation.
- **Directives:** Supports `p-if`, `p-else`, `p-for` (with `p-key`), `p-bind`, `p-show`, `p-text`, `p-html`, `p-model`, `p-on`, `p-pre`, `p-once`, `p-cloak`.
- **Template Inheritance & Macros:** Use `{{ extends }}`, `{{ include }}`, and `{{ macro }}` for modular templates.
- **Security:** Autoescaping and sandboxed environment for untrusted templates.
- **AsyncIO Support:** Render templates asynchronously with `render_template_async`.
- **I18N:** Babel integration for internationalization.
- **Performance:** Just-in-time compilation and caching for optimized rendering.
- **Extensibility:** Custom filters, tests, and functions.

## Example with I18N and AsyncIO

```python
from fleet import VueJinjaEngine
from babel.support import Translations

async def render():
    engine = VueJinjaEngine(sandboxed=True, enable_async=True, i18n_translations=Translations.load('translations', ['en']))
    with open('templates/index.html', 'r') as file:
        template = file.read()
    data = {'show': True, 'message': 'Hello', 'items': [{'id': 1, 'name': 'Item 1'}]}
    return await engine.render_template_async(template, data)
```

## Contributing

Contributions are welcome! Please submit issues or pull requests to the [GitHub repository](https://github.com/yourusername/fleet).

## License

MIT License
