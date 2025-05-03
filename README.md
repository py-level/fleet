# Fleet

[![PyPI version](https://badge.fury.io/py/fleetvue.svg)](https://badge.fury.io/py/fleetvue)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Fleet is a Python templating engine using Jinja2, mimicking Vue.js syntax. It uses `p-` directives (e.g., `p-if`, `p-for`) and `{{ }}` for control and interpolation, avoiding `{% %}`. Ideal for Python web projects, it enables dynamic, secure HTML rendering with a familiar client-server templating syntax.

## Features

* **Vue.js-Like Syntax:** Use `p-` directives and `{{ }}` for template control and interpolation
* **Directives Support:**
  * `p-if`, `p-else-if`, `p-else` for conditional rendering
  * `p-for` with `p-key` for list rendering
  * `p-bind` for attribute binding
  * `p-text` for text content
  * `p-html` for HTML content (with safe escaping)
  * `p-show` for conditional display
  * `p-model` for form input binding
  * `p-on` for event handling
  * `p-pre`, `p-once`, `p-cloak` for optimization
* **Security Features:**
  * Sandboxed environment for untrusted templates
  * Automatic HTML escaping
  * Safe rendering of HTML content
* **Advanced Features:**
  * AsyncIO support for asynchronous rendering
  * I18N support through Babel integration
  * Template inheritance and includes
  * Custom filters and functions
  * JIT compilation and caching

## Installation

```bash
pip install fleetvue
```

Required dependencies:
- jinja2>=3.0.0
- beautifulsoup4>=4.9.3

For I18N support (optional):
```bash
pip install babel
```

## Basic Usage

### Simple Template Example

```html
<div p-if="show">
    <h1 p-text="title"></h1>
    <p p-text="message"></p>
</div>
```

```python
from fleetvue import render_template

data = {
    'show': True,
    'title': 'Hello Fleet',
    'message': 'Welcome to Fleet templating!'
}

output = render_template(template, data)
```

### List Rendering Example

```html
<div class="user-list">
    <div p-for="user in users" p-key="user.id" class="user-card">
        <h3 p-text="user.name"></h3>
        <p p-text="user.role"></p>
        <ul>
            <li p-for="skill in user.skills" p-text="skill"></li>
        </ul>
    </div>
</div>
```

```python
data = {
    'users': [
        {
            'id': 1,
            'name': 'John Doe',
            'role': 'Developer',
            'skills': ['Python', 'JavaScript', 'Vue']
        },
        {
            'id': 2,
            'name': 'Jane Smith',
            'role': 'Designer',
            'skills': ['UI/UX', 'Figma', 'CSS']
        }
    ]
}
```

### Attribute Binding

```html
<img p-bind:src="imageUrl" p-bind:alt="imageAlt">
<a p-bind:href="link" p-text="linkText"></a>
```

### Custom Filters

```python
from fleetvue import VueJinjaEngine

engine = VueJinjaEngine()
engine.env.filters['double'] = lambda x: x * 2

template = '<div p-text="number | double"></div>'
data = {'number': 21}
result = engine.render_template(template, data)  # Outputs: <div>42</div>
```

### Async Rendering

```python
from fleetvue import VueJinjaEngine

async def render_async():
    engine = VueJinjaEngine(enable_async=True)
    template = '<div p-text="message"></div>'
    data = {'message': 'Hello World'}
    return await engine.render_template_async(template, data)
```

### Sandboxed Environment

```python
from fleetvue import VueJinjaEngine

engine = VueJinjaEngine(sandboxed=True)
template = '<div p-text="message | upper"></div>'
data = {'message': 'hello'}
result = engine.render_template(template, data)
```

## Integration with Web Frameworks

### Flask Integration

```python
from flask import Flask
from fleetvue import render_template

app = Flask(__name__)

@app.route('/')
def index():
    data = {
        'title': 'Welcome',
        'items': ['Item 1', 'Item 2', 'Item 3']
    }
    return render_template('templates/index.html', data)
```

### FastAPI Integration

```python
from fastapi import FastAPI
from fleetvue import VueJinjaEngine

app = FastAPI()
engine = VueJinjaEngine(enable_async=True)

@app.get("/")
async def index():
    data = {
        'title': 'Welcome',
        'items': ['Item 1', 'Item 2', 'Item 3']
    }
    return await engine.render_template_async('templates/index.html', data)
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Links

- GitHub: [https://github.com/py-level/fleet](https://github.com/py-level/fleet)
- PyPI: [https://pypi.org/project/fleetvue/](https://pypi.org/project/fleetvue/)
- Documentation: [Coming Soon]

## Author

Created and maintained by [py-level](https://github.com/py-level)

## Acknowledgments

- [Jinja2](https://jinja.palletsprojects.com/) for the powerful templating engine
- [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/) for HTML parsing
- [Vue.js](https://vuejs.org/) for the inspiration and syntax

# FleetVue Demo Project

This project demonstrates the usage of the FleetVue templating engine, which provides Vue.js-like syntax for Python templates.

## Setup

1. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Examples

### Basic Example
Run the basic example:
```bash
python example.py
```

This example demonstrates:
- Basic template rendering
- Vue-like directives (v-text, v-if, v-for)
- Event handling (v-on:click)
- Data binding

### Advanced Example
Run the advanced example:
```bash
python advanced_example.py
```

This example demonstrates:
- Custom filters
- Component registration and usage
- Advanced template features
- Data binding with filters
- Component props

## Features Demonstrated

- Vue-like directives (v-text, v-if, v-for, v-on, v-bind)
- Template interpolation with {{ }}
- Custom filters
- Component system
- Event handling
- Data binding
- Conditional rendering
- List rendering

## Learn More

For more information about FleetVue, visit:
https://pypi.org/project/fleetvue/ 