# Quick Start Guide

Get started with pyspade-native in 5 minutes!

## 1. Install

```bash
pip install pyspade-native
```

## 2. Verify Installation

```bash
python -m pyspade_native
```

You should see output like:
```
pyspade-native Installation Info
============================================================
Version: 0.1.0
Package directory: /path/to/site-packages/pyspade_native
Include directory: /path/to/site-packages/pyspade_native/include
Library directory: /path/to/site-packages/pyspade_native/lib
...
```

## 3. Use in Your Project

### Create a Simple Project

**Directory structure:**
```
my_project/
├── pyproject.toml
├── CMakeLists.txt
└── src/
    ├── my_package/
    │   └── __init__.py
    └── cpp/
        └── my_module.cpp
```

**pyproject.toml:**
```toml
[build-system]
requires = ["scikit-build-core", "pybind11", "pyspade-native"]

[project]
name = "my-package"
version = "0.1.0"
dependencies = ["pyspade-native"]
```

**CMakeLists.txt:**
```cmake
cmake_minimum_required(VERSION 3.15)
project(my_package)

find_package(Python REQUIRED COMPONENTS Interpreter Development)
find_package(pybind11 CONFIG REQUIRED)

# Find pyspade-native
execute_process(
    COMMAND ${Python_EXECUTABLE} -c "import pyspade_native; print(pyspade_native.get_cmake_dir())"
    OUTPUT_VARIABLE PYSPADE_CMAKE_DIR
    OUTPUT_STRIP_TRAILING_WHITESPACE
)
find_package(pyspade_native REQUIRED PATHS ${PYSPADE_CMAKE_DIR} NO_DEFAULT_PATH)

# Create your extension
pybind11_add_module(my_module src/cpp/my_module.cpp)
target_link_libraries(my_module PRIVATE pyspade_native::spade_wrapper)
install(TARGETS my_module DESTINATION .)
```

**src/cpp/my_module.cpp:**
```cpp
#include <pybind11/pybind11.h>
#include <spade_wrapper.h>

namespace py = pybind11;

void example_triangulate() {
    std::vector<spade::Point> polygon = {
        {0.0, 0.0, 0.0},
        {1.0, 0.0, 0.0},
        {0.5, 1.0, 0.0}
    };

    auto result = spade::triangulate(
        polygon, {}, {}, 0.5,
        spade::Quality::Moderate, true
    );

    py::print("Triangulated! Vertices:", result.num_vertices());
}

PYBIND11_MODULE(my_module, m) {
    m.def("triangulate", &example_triangulate);
}
```

### Build and Test

```bash
pip install .
python -c "from my_package import my_module; my_module.triangulate()"
```

## 4. Explore Examples

See the [complete example project](examples/complete-project/README.md) for a full working implementation.

## Next Steps

- Read the [CMake Integration Guide](docs/cmake.md)
- Check the [C++ API Reference](docs/api.md)
- Browse [examples](examples/)
- Join discussions on GitHub

## Troubleshooting

**Problem:** `pyspade_native not found`
**Solution:** Make sure it's in your build requirements:
```toml
[build-system]
requires = ["pyspade-native>=0.1.0", ...]
```

**Problem:** CMake can't find pyspade_native
**Solution:** Verify Python can import it:
```bash
python -c "import pyspade_native; print(pyspade_native.get_cmake_dir())"
```

**Problem:** Linking errors
**Solution:** Use the CMake target:
```cmake
target_link_libraries(your_target PRIVATE pyspade_native::spade_wrapper)
```

## Get Help

- [Documentation](https://dtcc-platform.github.io/pyspade-native/)
- [GitHub Issues](https://github.com/dtcc-platform/pyspade-native/issues)
- [Discussions](https://github.com/dtcc-platform/pyspade-native/discussions)