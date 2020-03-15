**Work in Progress!**

PyTCC shall become a python extension that contains 
[TCC](https://en.wikipedia.org/wiki/Tiny_C_Compiler), 
a full fledged C compiler from Fabrice Bellard.

In a first step it will only be a one to one adaption of the API
of TCC's tcclib. This library allows not only generating executables and 
libraries, but also running the generated code in the addressspace
of the current process without the need of creating a new file.

Current status:
* Supports 32bit Python on Windows
* Provide tcclib API in Python

Roadmap:
* Create Wheels for all platforms
* MAYBE: Make it Crossplatform
* MAYBE: Extend TCC (and PyTCC) to provide access to AST


# Howto Build

To build this extension the following software (apart from python) is
required as prerequisites:
* CMake
* C Compiler
* tox *[OPTIONAL]*

First of all you have to build the TCC binaries by running cmake to
create your platform specific project files and then build your project
files. In a second step you build the python C-extension via setup.py

```
>> cmake -A x64 -B tinycc-bin\win64
>> cmake --build tinycc-bin\win64 --config Release
>> tox
```

If you build on linux or mac replace "win64" by "linux64" or "mac64";
To build on 32bit architecture replace "win64" by "win32" and "x64" by "Win32".

Alternatively you could choose any directory as output for the TCC binary and
set the environment variable ``TCC_BUILD_DIR`` to the corresponding directory.


# Howto debug

To debug pytcc it is recommended to run cmake when the python environment
that shall be used for the tests is activated (i.e. after running tox you
could manually do this via ``.tox/py36/Scripts/activate``).
Cmake will then create a additional target: "pytcc".
This one can be used for creating the C extention without setup.py.
As cmake is supported by most C IDEs you can use the resulting project file
to debug the project.
