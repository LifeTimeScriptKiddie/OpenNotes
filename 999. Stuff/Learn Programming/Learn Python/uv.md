---
dg-publish: true
---

A fast python package installer and resolver in Rust. 
Aims to replace pip, pip-tools, and virtualenv.


Replaces
	pip install
	pip-tools, pip-compile, pip-sync
	virtualenv

# Install
```
curl -Ls https://astral.sh/uv/install.sh |bash
pipx install uv
```

# Common usage -Venv
```python
uv venv

source .venv/bin/activate # Linux/Mac
.\.venv\Script\activate # Windows
```
# Installing packages
```python
uv pip install request

uv pip install -r requirements.txt
```

# Freeze installed packages
```python
uv pip freeze > requirements.txt

```

# Compile dependencies
```python
uv pip compile pyproject.toml
```