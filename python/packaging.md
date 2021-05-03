## Packaging

*Disclaimer: Info sourced from [this video](https://www.youtube.com/watch?v=4fzAMdLKC5k) and from [this guide](https://packaging.python.org/tutorials/packaging-projects/)*

### Goal
We want to pacakge our Python project into a downloadable service similar to that of `boto3`.

### Definitions
* **module** - saved python code in a file
* **package** - namespace used to organize code (directory with `__init__.py`)
* **distribution package** - bundled python code, which is downloaded from PyPI (built and source distributions)
* **source distribution** - raw bundled source
* **built distribution** - compiled built source (wheel)
* **PiPI** - package index

### Components
* **code** - the functionality that you want to share
* **`setup.py`** - holds metadata of package and is a script that facilitates the packaging
* **`setup.cfg`** - configuration for wheel and setup script
* **`MANIFEST.in`** - specification of anything in the package that should be included besides python code and explicit data

### Key Pieces of `setup.py`
```python
from setuptools import setup, find_packages

with open("README.md", "r", encoding="utf-8") as fh:
    long_description = fh.read()

setuptools.setup(
    name="",
    version="",
    author="",
    author_email="",
    description="",
    long_description=long_description, # generated above from README.md and shown on PyPI
    long_description_content_type="text/markdown",
    url="",
    project_urls={}, # any other links to show on PyPI
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    package_dir={"": "src"},
    package_data={ # specifies other files to include that aren't Python files, but are needed by the project - different from MANIFEST.in, which usually holds non-code files - THIS IS RELATIVE PATH
        "sample": ["package_data.dat"]
    }
    data_files=None # similar to package_data but absolute path
    install_requires=["boto3", "requests"], # dependencies of project
    packages=setuptools.find_packages(where="src", exlude=["tests*"]), # finds all Python packages to include, exclude only pertains to built distributions
    python_requires=">=3.6",
)
```