# CLAUDE.md

This file provides instructions for Claude when working with this repository.

## MANDATORY: Context7 MCP Server Consultation

**IMPORTANT**: When working on this repository, you MUST always consult the context7 MCP server for best practices and current patterns. If the context7 MCP server is not available, you MUST explicitly notify the user that you cannot access it and that this may impact the quality of your analysis.

### Required Consultations

When performing ANY of the following tasks, you MUST check context7:

1. **Packaging Review**
   - Search for `setuptools` best practices for native extensions
   - Search for `scikit-build-core` patterns and examples
   - Compare complexity with similar projects
   - Look for simpler alternatives to current patterns

2. **Build System Analysis**
   - Check CMake patterns for library distribution
   - Review binary packaging strategies
   - Examine platform-specific build configurations
   - Search for wheel building best practices

3. **Code Architecture Review**
   - Compare with similar C++/Python hybrid packages
   - Look for overengineering patterns
   - Find examples of binary distribution via PyPI
   - Check for git-installable package patterns

4. **Dependency Management**
   - Review Python packaging best practices
   - Check for modern alternatives to current approach
   - Validate build system choices

### Error Handling

If you cannot access the context7 MCP server, you MUST:
1. Immediately inform the user: "⚠️ I cannot access the context7 MCP server, which is required for proper analysis of this repository."
2. Explain what information you're missing
3. Proceed with limited analysis but note the limitations

### Specific Queries to Run

For packaging reviews, always run these context7 queries:
- Library: `setuptools` - Topic: "native extensions packaging cmake"
- Library: `scikit-build-core` - Topic: "cmake binary distribution"
- Library: `cibuildwheel` - Topic: "platform wheels native libraries"

### Review Checklist

When reviewing this repository, use context7 to validate:
- [ ] Is the three-tier build strategy (local → download → build) standard practice?
- [ ] Are there simpler examples of distributing C++ via PyPI?
- [ ] What's the recommended way to handle git+https installations?
- [ ] Are there better patterns for platform-specific binary distribution?
- [ ] Is the current CMake complexity justified?

## Project-Specific Context

This is a Python package (`dtcc-pyspade-native`) that distributes a C++ library (Spade triangulation) via PyPI without Python bindings. Key requirements:
- Must work with `pip install dtcc-pyspade-native` (from PyPI)
- Must work with `pip install git+https://github.com/dtcc-platform/dtcc-pyspade-native`
- No Python bindings - pure C++ library distribution
- No C++ package manager usage desired
- Targets users who have C++ extensions that need this library

Always validate architectural decisions against these constraints using context7 examples.