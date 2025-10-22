# Contributing to dtcc-pyspade-native

Thank you for your interest in contributing to dtcc-pyspade-native!

## Development Setup

### Prerequisites

- Python 3.8+
- C++ compiler with C++17 support
- CMake 3.15+
- Rust toolchain (https://rustup.rs/)
- Git

### Clone and Install

```bash
git clone https://github.com/dtcc-platform/dtcc-pyspade-native
cd dtcc-pyspade-native
pip install -e ".[dev]"
```

## Making Changes

### Code Style

- Python code: Follow PEP 8
- C++ code: Follow Google C++ Style Guide
- Rust code: Run `cargo fmt`
- CMake: Use consistent indentation (4 spaces)

### Testing

Before submitting a PR:

```bash
# Test installation
python -m pyspade_native

# Build and test the example
cd examples/complete-project
pip install .
python test_example.py
cd ../..

# Build wheels locally
python -m build
```

### Documentation

- Update README.md if adding features
- Add docstrings to Python functions
- Comment complex C++ code
- Update CHANGELOG.md

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly
5. Commit with clear messages
6. Push to your fork
7. Open a Pull Request

### PR Checklist

- [ ] Code follows style guidelines
- [ ] Tests pass locally
- [ ] Documentation updated
- [ ] CHANGELOG.md updated
- [ ] Commits are clear and atomic

## Reporting Issues

### Bug Reports

Include:
- Python version
- Operating system
- Steps to reproduce
- Expected vs actual behavior
- Error messages/stack traces

### Feature Requests

Describe:
- Use case
- Proposed solution
- Alternatives considered
- Impact on existing users

## Release Process

(For maintainers)

1. Update version in `pyproject.toml`
2. Update CHANGELOG.md
3. Create git tag: `git tag v0.x.0`
4. Push tag: `git push origin v0.x.0`
5. GitHub Actions will build and publish to PyPI

## Code of Conduct

Be respectful and inclusive. We're all here to learn and improve.

## Questions?

Open an issue or discussion on GitHub!