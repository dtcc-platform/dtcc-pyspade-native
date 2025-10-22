# Example: Using pyspade-native in a Python Project

This example demonstrates how to use the `pyspade-native` package in a Python project that has C++ components.

## What This Example Shows

- How to depend on `pyspade-native` in `pyproject.toml`
- How to find and link the Spade C++ library using CMake
- How to use Spade triangulation in your C++ code
- How to expose the functionality to Python via pybind11

## Structure

```
example_usage/
├── pyproject.toml          # Python package configuration
├── CMakeLists.txt          # CMake build configuration
├── src/
│   ├── example_pkg/
│   │   └── __init__.py     # Python package
│   └── cpp/
│       └── geometry_binding.cpp  # C++ module using Spade
└── test_example.py         # Test script
```

## Building and Running

### Prerequisites

1. Install pyspade-native:
   ```bash
   pip install pyspade-native
   ```

   Or if building from local source:
   ```bash
   cd ../  # Go to pyspade-native directory
   pip install .
   cd example_usage
   ```

### Build the Example

```bash
pip install .
```

### Run the Test

```bash
python test_example.py
```

Expected output:
```
Testing pyspade-native integration...
Input polygon: (4, 2)
Output vertices: 15
Output triangles: 20
Vertices shape: (15, 3)
Triangles shape: (20, 3)

First few triangles:
  Triangle 0: [1 5 0]
  Triangle 1: [2 6 1]
  Triangle 2: [3 7 2]

✓ Test passed! pyspade-native is working correctly.
```

## Key Files Explained

### `pyproject.toml`

Specifies dependencies on `pyspade-native`:

```toml
[build-system]
requires = [
    "pyspade-native>=0.1.0",  # Build-time dependency
    ...
]

[project]
dependencies = [
    "pyspade-native>=0.1.0",  # Runtime dependency
]
```

### `CMakeLists.txt`

Finds and links the Spade library:

```cmake
# Get pyspade-native CMake directory from Python
execute_process(
    COMMAND ${Python_EXECUTABLE} -c
        "import pyspade_native; print(pyspade_native.get_cmake_dir())"
    OUTPUT_VARIABLE PYSPADE_CMAKE_DIR
)

# Find pyspade-native package
find_package(pyspade_native REQUIRED PATHS ${PYSPADE_CMAKE_DIR})

# Link your module with Spade
target_link_libraries(your_module PRIVATE pyspade_native::spade_wrapper)
```

### `geometry_binding.cpp`

Uses Spade C++ API:

```cpp
#include <spade_wrapper.h>  // From pyspade-native

// Use Spade in your C++ code
auto result = spade::triangulate(
    polygon,
    {},  // holes
    {},  // interior_loops
    max_edge_length,
    spade::Quality::Moderate,
    true
);
```

## Integration with Your Project

To use this pattern in your own project:

1. **Add pyspade-native to your dependencies:**
   - In `pyproject.toml` build-system requires
   - In `pyproject.toml` project dependencies

2. **Update your CMakeLists.txt:**
   - Add the pyspade-native finding code
   - Link your targets with `pyspade_native::spade_wrapper`

3. **Use Spade in your C++ code:**
   - Include `<spade_wrapper.h>`
   - Use the `spade::` namespace functions

4. **No need to:**
   - Manually install Spade
   - Build Spade separately
   - Configure Rust
   - Worry about platform differences

The `pyspade-native` package handles all of that automatically!