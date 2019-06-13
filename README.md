# python-example-package
Packaging example for PyPi

## Detailed tutorial 
[Packaging python project](https://packaging.python.org/tutorials/packaging-projects/)

## Project structure
```
/toplevel_dir
    /example_pkg
        __init__.py
    setup.py
    LICENSE
    README.md
```
`example_pkg` directory contains all the source code. All other files are described below. 

## Important steps

1. (Assuming you have the working project) Create the supporting files -

- Create `setup.py`

```
import setuptools

with open("README.md", "r") as fh:
    long_description = fh.read()

setuptools.setup(
    name="example-pkg-amoghskulkarni",
    version="0.0.1",
    author="Amogh Kulkarni",
    author_email="amoghkulkarni.kop@gmail.com",
    description="A small example package",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="https://github.com/amoghskulkarni/python-example-package",
    packages=setuptools.find_packages(),
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
)
``` 

Change all the fields as suited to your project, and save.

- Create `README.md`
    
Not necessary if your project already contains one. 

- Create `LICENSE`

When in doubt, use MIT.

```
Copyright (c) 2018 The Python Packaging Authority

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

2. Generate distribution archives

Replace `python3` with `python` in case you're using Python 2.7.

- Upgrade `setuptools` and `wheel` 

```
python3 -m pip install --user --upgrade setuptools wheel
```

- Create/build distribution

```
python3 setup.py sdist bdist_wheel
```

This will create a `/dist` directory and it will have built distribution in it. 

3. Upload 

Replace `python3` and `python` in case you're using Python 2.7. 

- Install `twine`

```
python3 -m pip install --user --upgrade twine
```

- Run `twine` to upload

```
python3 -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
```

4. Install your package 

Following command is for TestPyPi, seperate instance of PyPi, meant for testing purposes.

```
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-pkg-amoghskulkarni
```