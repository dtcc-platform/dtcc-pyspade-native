# pyspade-native - Fresh Repository

This directory contains a **complete, ready-to-publish** standalone repository for `pyspade-native`.

## What's Inside

A production-ready Python package that ships the Spade C++ triangulation library:

```
new-repo/
├── .github/workflows/    # CI/CD for building and publishing
├── cmake/                # CMake package configuration
├── cppspade/            # The C++ Spade wrapper library
├── docs/                # Documentation (placeholder)
├── examples/            # Complete working example
├── scripts/             # Build and test scripts
├── src/pyspade_native/  # Python helper module
├── tests/               # Basic tests
├── pyproject.toml       # Modern Python packaging
├── CMakeLists.txt       # Build configuration
├── LICENSE              # Dual MIT/Apache-2.0
├── README.md            # Main documentation
├── QUICKSTART.md        # Quick start guide
├── CONTRIBUTING.md      # Contribution guidelines
├── CHANGELOG.md         # Version history
└── SETUP_NEW_REPO.md    # Repository initialization guide
```

## Quick Start

### 1. Create New Repository

Follow instructions in `SETUP_NEW_REPO.md`

### 2. Test Locally

```bash
cd new-repo

# Build and install
pip install -e .

# Verify
python -m pyspade_native

# Test example
cd examples/complete-project
pip install .
python test_example.py
```

### 3. Publish

```bash
# Build package
./scripts/build.sh

# Publish to PyPI
pip install twine
twine upload dist/*
```

## Repository Features

✅ **Production Ready**
- Modern `pyproject.toml` configuration
- Cross-platform wheel building
- Automated CI/CD with GitHub Actions
- Comprehensive documentation

✅ **Easy Integration**
- CMake `find_package()` support
- Python helper API
- Complete working examples
- Clear error messages

✅ **Well-Maintained**
- Testing setup
- Contributing guidelines
- Changelog template
- Issue templates ready

✅ **Cross-Platform**
- Linux (x86_64, ARM64)
- macOS (Intel, Apple Silicon, Universal)
- Windows (x86_64)

## What Users Get

When someone runs `pip install pyspade-native`:

1. **C++ Libraries**: spade_wrapper + spade_ffi
2. **Headers**: All Spade C++ API headers
3. **CMake Config**: For easy `find_package()`
4. **Python Helpers**: Path discovery functions
5. **No Dependencies**: Self-contained package

## Use Case

Perfect for Python packages with C++ extensions that need triangulation:

```python
# Their pyproject.toml
[build-system]
requires = ["scikit-build-core", "pybind11", "pyspade-native"]

[project]
dependencies = ["pyspade-native"]
```

```cmake
# Their CMakeLists.txt
find_package(pyspade_native REQUIRED)
target_link_libraries(their_module PRIVATE pyspade_native::spade_wrapper)
```

```cpp
// Their C++ code
#include <spade_wrapper.h>
auto result = spade::triangulate(polygon, {}, {}, 1.0, spade::Quality::Moderate, true);
```

## Next Steps

1. Read `SETUP_NEW_REPO.md` for repository initialization
2. Customize as needed for your organization
3. Test thoroughly before publishing
4. Follow semantic versioning for releases

## Support

This is a standalone package ready for independent publication and maintenance.

For questions about usage, see the main README.md and examples/.

---

**Ready to commit as a fresh repository!** 🚀
