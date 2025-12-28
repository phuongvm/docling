# Docling: Task Completion Checklist

## Standard Task Completion Workflow

When completing a development task, follow this sequence:

### 1. Code Formatting
**Command:**
```powershell
uv run ruff format docling tests
```

**What it does:**
- Formats all Python code according to project style (88 char line length)
- Auto-fixes formatting issues

**Note:** If files are modified, you'll need to stage them with `git add` before committing.

### 2. Linting
**Command:**
```powershell
uv run ruff check --fix docling tests
```

**What it does:**
- Runs Ruff linter with auto-fix enabled
- Fixes common issues automatically
- Reports remaining issues that need manual attention

**Note:** Some issues may require manual fixes. Review the output.

### 3. Type Checking
**Command:**
```powershell
uv run mypy docling
```

**What it does:**
- Validates type hints throughout the codebase
- Uses Pydantic plugin for model validation
- Reports type errors

**Note:** Some third-party modules are ignored (configured in pyproject.toml).

### 4. Testing
**Command:**
```powershell
uv run pytest
```

**What it does:**
- Runs the full test suite
- Validates that existing functionality still works
- Ensures new code doesn't break existing tests

**For new features:**
- Add tests in appropriate test file
- Follow existing test patterns
- Test both success and error cases

### 5. Pre-commit Validation (Recommended)
**Command:**
```powershell
uv run pre-commit run --all-files
```

**What it does:**
- Runs all pre-commit hooks (Ruff formatter, Ruff linter, MyPy, uv-lock)
- Simulates what will run on commit
- Ensures code quality before committing

**Note:** If hooks modify files, stage them and commit again.

## Special Cases

### When Adding New Dependencies
1. Add dependency: `uv add <package-name>`
2. Update pyproject.toml and uv.lock automatically
3. Run tests to ensure compatibility
4. Update documentation if needed

### When Modifying Test Reference Data
**WARNING:** Requires double review!

**Command:**
```powershell
$env:DOCLING_GEN_TEST_DATA=1; uv run pytest
```

**Process:**
1. Regenerate reference data with above command
2. Review all changes carefully
3. Ensure changes are intentional improvements
4. Get second reviewer approval before merging

### When Updating Documentation
1. Edit Markdown files in `docs/`
2. Test locally: `uv run mkdocs serve`
3. Verify links and formatting
4. Build: `uv run mkdocs build`
5. Deploy if needed: `uv run mkdocs gh-deploy`

### When Working with CLI
1. Test CLI changes: `uv run docling --help`
2. Test with sample documents
3. Verify output formats
4. Update CLI tests if needed

## Quality Gates

Before considering a task complete:

- ✅ Code is formatted (Ruff format passes)
- ✅ Linting passes (Ruff check passes)
- ✅ Type checking passes (MyPy passes)
- ✅ All tests pass (pytest passes)
- ✅ New code has tests (if applicable)
- ✅ Documentation updated (if applicable)
- ✅ Pre-commit hooks pass (recommended)

## Git Workflow

### Before Committing
1. Run all quality checks (format, lint, type, test)
2. Stage modified files: `git add .`
3. If pre-commit modified files, stage again: `git add .`

### Commit Message Format
Follow semantic release conventions:
- `feat:` - New feature (minor version bump)
- `fix:` - Bug fix (patch version bump)
- `perf:` - Performance improvement (patch version bump)
- `docs:` - Documentation changes
- `style:` - Code style changes
- `refactor:` - Code refactoring
- `test:` - Test additions/changes
- `chore:` - Maintenance tasks
- `ci:` - CI/CD changes
- `build:` - Build system changes

**Example:**
```
feat: add support for WebVTT file parsing
fix: resolve PDF table extraction issue
docs: update installation instructions
```

## Common Issues and Solutions

### Ruff modifies files on commit
**Solution:** This is expected. Stage the modified files and commit again.

### MyPy errors in third-party code
**Solution:** These are ignored by configuration. Focus on errors in `docling/` package.

### Tests fail after dependency update
**Solution:** 
1. Check if dependency version is compatible
2. Review changelog of updated dependency
3. Update test expectations if needed

### Pre-commit hook fails
**Solution:**
1. Review the error message
2. Fix the issue manually
3. Run pre-commit again
4. If it's a false positive, discuss with team

## Final Checklist

Before marking task as complete:
- [ ] All code quality checks pass
- [ ] Tests pass (including new tests for new features)
- [ ] Documentation updated (if needed)
- [ ] Code reviewed (if required by team)
- [ ] Commit message follows conventions
- [ ] No sensitive data committed
- [ ] No large files committed (use Git LFS if needed)