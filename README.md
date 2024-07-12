# Sublime Dependencies 
There are a couple of ways to add some dependencies in sublime.
- Add the dependency to the dependencies.json, which needs to be in the [package control channel](https://github.com/packagecontrol/channel/blob/main/repository.json)
- Vendoring
# Vendoring
If the package imports all are relative you just need to add it to the _pieces_lib directory otherwise, you will need to use [vendoring](https://pypi.org/project/vendoring/) tool. **Download it from GitHub not pip**
pyproject.toml
```toml
[tool.vendoring]
	destination = "_pieces_lib"
	requirements = "vendor.txt"
	namespace = "Pieces._pieces_lib"
	protected-files = ["README.rst", "vendor.txt"]
	patches-dir = "tools/vendoring/patches"

```
These are the configurations that need to be inserted in the pyproject.toml, You also need to update the vendor.txt for the dependencies that you need to add as in the [example](https://github.com/pypa/pip/blob/main/src/pip/_vendor/vendor.txt).

Sometimes you will need to create a patch file to resolve some import issues that can’t be done via the tool, you will add the patch to the dir defined in the pyproject.toml in this case it will be “tools/vendoring/patches”

To begin vendoring you should do the following:

```bash
vendoring sync
```

To update the current lib:
```bash
vendoring update
```

Now on sublime, you will need to do
```python
from ._pieces_lib import pieces_os_client
```
Instead of 
```python
import pieces_os_client
```

