# Setting Up the New Repository

Follow these steps to initialize and publish the pyspade-native repository.

## 1. Initialize Git Repository

```bash
cd new-repo
git init
git add .
git commit -m "Initial commit: pyspade-native package"
```

## 2. Create GitHub Repository

1. Go to https://github.com/dtcc-platform
2. Click "New repository"
3. Name: `pyspade-native`
4. Description: "Spade C++ triangulation library packaged for Python projects"
5. Keep it public
6. Don't initialize with README (we have one)
7. Click "Create repository"

## 3. Push to GitHub

```bash
git remote add origin git@github.com:dtcc-platform/pyspade-native.git
git branch -M main
git push -u origin main
```

## 4. Configure GitHub Repository

### Enable GitHub Actions
1. Go to Settings → Actions → General
2. Enable "Allow all actions and reusable workflows"
3. Save

### Add PyPI Secrets (for publishing)
1. Go to Settings → Secrets and variables → Actions
2. Add secrets:
   - `PYPI_API_TOKEN` - Your PyPI API token
   - `TEST_PYPI_API_TOKEN` - Your Test PyPI API token

To get PyPI tokens:
- PyPI: https://pypi.org/manage/account/token/
- Test PyPI: https://test.pypi.org/manage/account/token/

### Enable GitHub Pages (optional, for docs)
1. Go to Settings → Pages
2. Source: Deploy from a branch
3. Branch: gh-pages (will be created by docs workflow)

## 5. Test Local Build

```bash
# Install in development mode
pip install -e .

# Test Python API
python -m pyspade_native

# Run tests
pip install pytest
pytest tests/

# Test example
cd examples/complete-project
pip install .
python test_example.py
cd ../..
```

## 6. Create First Release

### Option A: Manual Release

```bash
# Build the package
./scripts/build.sh

# Test upload to Test PyPI (optional)
pip install twine
twine upload --repository testpypi dist/*

# Test install from Test PyPI
pip install --index-url https://test.pypi.org/simple/ pyspade-native

# Upload to PyPI
twine upload dist/*
```

### Option B: Automated Release via GitHub

1. Create and push a tag:
   ```bash
   git tag v0.1.0
   git push origin v0.1.0
   ```

2. Go to GitHub → Releases → "Create a new release"
3. Choose tag `v0.1.0`
4. Title: "v0.1.0 - Initial Release"
5. Description: Copy from CHANGELOG.md
6. Click "Publish release"

GitHub Actions will automatically:
- Build wheels for all platforms
- Run tests
- Publish to PyPI (if secrets are configured)

## 7. Verify Installation

```bash
# Install from PyPI
pip install pyspade-native

# Verify
python -c "import pyspade_native; pyspade_native.print_info()"
```

## 8. Update Documentation

After first release:

1. Update README badges with actual PyPI link
2. Add link to published documentation
3. Update examples with actual install commands
4. Announce on relevant forums/communities

## 9. Set Up Project Management

### GitHub Issues Templates
Create `.github/ISSUE_TEMPLATE/`:
- `bug_report.md`
- `feature_request.md`

### GitHub Discussions
Enable Discussions in Settings for:
- Q&A
- Show and tell
- Ideas

### Branch Protection
Settings → Branches → Add rule for `main`:
- Require pull request reviews
- Require status checks to pass
- Require branches to be up to date

## 10. Ongoing Maintenance

### For Each New Version

1. Update `pyproject.toml` version
2. Update `CHANGELOG.md`
3. Commit changes
4. Create and push tag:
   ```bash
   git tag v0.x.0
   git push origin v0.x.0
   ```
5. Create GitHub release
6. GitHub Actions handles the rest!

### Regular Tasks

- Monitor GitHub Issues
- Review Pull Requests
- Update dependencies
- Test with new Python versions
- Keep documentation current

## Troubleshooting

### Build Fails in GitHub Actions

- Check Rust installation step
- Verify CMake configuration
- Check platform-specific dependencies

### PyPI Upload Fails

- Verify API tokens in GitHub Secrets
- Check version number (must be unique)
- Ensure package builds locally first

### Users Report Import Errors

- Verify wheel includes all libraries
- Check MANIFEST.in includes all needed files
- Test installation on clean environment

## Need Help?

- Check existing GitHub Issues
- Review GitHub Actions logs
- Test locally with same Python version
- Ask in GitHub Discussions

## Success Checklist

- [ ] Git repository initialized
- [ ] Pushed to GitHub
- [ ] GitHub Actions enabled
- [ ] PyPI secrets configured
- [ ] Local build works
- [ ] Tests pass
- [ ] Example project works
- [ ] First release published to PyPI
- [ ] Installation from PyPI verified
- [ ] Documentation accessible
- [ ] Repository well-organized

Congratulations! Your pyspade-native repository is ready to use! 🎉