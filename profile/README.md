<p align="center">
  <a href="https://dynaconf.com"><img src="https://github.com/dynaconf/dynaconf/raw/master/docs/img/logo_400.svg?sanitize=true" alt="Dynaconf" width="600px"></a>
</p>
<p align="center">
    <strong>Dynaconf</strong> is <em>Configuration Management for Python.</em>
</p>

<p align="center"><a href="/LICENSE"><img alt="MIT License" src="https://img.shields.io/badge/license-MIT-007EC7.svg?style=flat-square"></a> <a href="https://pypi.python.org/pypi/dynaconf"><img alt="PyPI" src="https://img.shields.io/pypi/v/dynaconf.svg"></a><a href="https://github.com/rochacbruno/dynaconf/actions/workflows/main.yml"><img src="https://github.com/rochacbruno/dynaconf/actions/workflows/main.yml/badge.svg"></a><a href="https://codecov.io/gh/rochacbruno/dynaconf"><img alt="codecov" src="https://codecov.io/gh/rochacbruno/dynaconf/branch/master/graph/badge.svg"></a> <a href="https://www.codacy.com/gh/rochacbruno/dynaconf/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=rochacbruno/dynaconf&amp;utm_campaign=Badge_Grade"><img src="https://app.codacy.com/project/badge/Grade/42d2f11ef0a446808b246c8c69603f6e"/></a> <img alt="GitHub Release Date" src="https://img.shields.io/github/release-date/rochacbruno/dynaconf.svg"> <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/rochacbruno/dynaconf.svg"> <a href="https://github.com/rochacbruno/dynaconf/discussions"><img alt="Discussions" src="https://img.shields.io/badge/discussions-forum-yellow.svg?logo=googlechat"></a> <a href="https://github.com/rochacbruno/learndynaconf"><img alt="Demo" src="https://img.shields.io/badge/demo-learn-blue.svg?logo=gnubash"></a></p>


## Features

- Inspired by the **[12-factor application guide](https://12factor.net/config)**
- **Settings management** (default values, validation, parsing, templating)
- Protection of **sensitive information** (passwords/tokens)
- Multiple **file formats** `toml|yaml|json|ini|py` and also customizable loaders.
- Full support for **environment variables** to override existing settings (dotenv support included).
- Optional layered system for **multi environments** `[default, development, testing, production]` (also called multi profiles)
- Built-in support for **Hashicorp Vault** and **Redis** as settings and secrets storage.
- Built-in extensions for **Django** and **Flask** web frameworks.
- **CLI** for common operations such as `init, list, write, validate, export, get`.

## Installation

### Install from [pypi](https://pypi.org/project/dynaconf)

```bash
pip install dynaconf
```

Read the docs on [Dynaconf.com](https://dynaconf.com)

### Quick Start

> Looking for [Flask](https://www.dynaconf.com/flask/) or [Django](https://www.dynaconf.com/django/) plugins?

`config.py`
```python
from dynaconf import Dynaconf
settings = Dynaconf(
    envvar_prefix="APP", 
    settings_files=["default_settings.toml"], 
    environments=["production", "development"]
)
```

`default_settings.toml` (yaml, ini, json, py, cfg, etc...)
```toml
[default]
name = "Default Name"
debug = true
data = {value=1}

[development]
name = "amber"

[production]
debug = false
name = "@vault /take/from/vault/secret"
```

`main.py`
```python
from config import settings

if settings.debug:
    print(f"Hello {settings.name}")

print(settings.data.value)
print(settings.get("key", default="a default value for you"))
print(settings["NAME"], ", this also works as a dict")
```
---

`console`
```console
$ python main.py
Hello amber
1
a default value for you
amber, this also works as a dict

# Environment Variables overrides
$ APP_NAME=Bruno python main.py 
Hello Bruno

# Nested env vars works
$ APP_NAME=admin APP_DATA__VALUE=42 python main.py 
Hello admin
42
```

[Try it online](https://replit.com/@rochacbruno/dynaconf2020?v=1)

Read the docs on [Dynaconf.com](https://dynaconf.com)

