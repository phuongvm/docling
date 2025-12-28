# Docling: Suggested Commands

## Environment Setup

### Install uv (if not already installed)
```powershell
# On Windows, install via pip or download from https://github.com/astral-sh/uv
pip install uv
# Or use the installer from https://docs.astral.sh/uv/getting-started/installation/
```

### Create and sync virtual environment
```powershell
# Create venv and sync dependencies
uv sync

# Use specific Python version (optional)
uv venv --python 3.12
uv sync
```

### Install with optional dependencies
```powershell
# Install with all extras
uv sync --all-extras

# Install specific extras
uv sync --extra vlm --extra asr --extra easyocr
```

## Development Commands

### Add new dependency
```powershell
uv add <package-name>
# Example: uv add requests
```

### Run code formatter (Ruff)
```powershell
# Format code
uv run ruff format docling tests

# Check formatting without modifying
uv run ruff format --check docling tests
```

### Run linter (Ruff)
```powershell
# Lint and auto-fix
uv run ruff check --fix docling tests

# Lint without fixing
uv run ruff check docling tests
```

### Run type checker (MyPy)
```powershell
uv run mypy docling
```

### Run all pre-commit checks
```powershell
# Install pre-commit hooks (one-time setup)
uv run pre-commit install

# Run all checks manually
uv run pre-commit run --all-files
```

## Testing Commands

### Run all tests
```powershell
uv run pytest
```

### Run tests with coverage
```powershell
uv run pytest --cov=docling --cov-report=html
```

### Run specific test file
```powershell
uv run pytest tests/test_cli.py
```

### Run specific test function
```powershell
uv run pytest tests/test_cli.py::test_cli_help
```

### Run tests with verbose output
```powershell
uv run pytest -v
```

### Run tests and show durations
```powershell
uv run pytest --durations=0
```

### Regenerate reference test data
```powershell
# WARNING: This regenerates test reference data - requires double review
$env:DOCLING_GEN_TEST_DATA=1; uv run pytest
```

### Run tests excluding ML-heavy tests
```powershell
# Exclude ML tests (faster)
uv run pytest --ignore=tests/test_e2e_conversion.py --ignore=tests/test_e2e_ocr_conversion.py
```

## CLI Commands

### Run docling CLI
```powershell
# Convert a document
uv run docling <document-path-or-url>

# Convert with VLM pipeline
uv run docling --pipeline vlm --vlm-model granite_docling <document>

# Show help
uv run docling --help

# Show version
uv run docling --version
```

### Run docling-tools CLI
```powershell
uv run docling-tools --help
```

## Documentation Commands

### Serve documentation locally
```powershell
# Start MkDocs server
uv run mkdocs serve
# Server available at http://localhost:8000
```

### Build documentation
```powershell
uv run mkdocs build
```

### Deploy documentation to GitHub Pages
```powershell
uv run mkdocs gh-deploy
```

## Windows-Specific Commands

### PowerShell equivalents
```powershell
# List files
Get-ChildItem
# or: ls, dir

# Change directory
Set-Location <path>
# or: cd <path>

# Find files
Get-ChildItem -Recurse -Filter "*.py"
# or: Get-ChildItem -Recurse | Where-Object {$_.Name -like "*.py"}

# Search in files
Select-String -Path "*.py" -Pattern "pattern"
# or: grep equivalent

# Git commands (same as Unix)
git status
git add .
git commit -m "message"
```

## Task Completion Checklist

When completing a task, run these commands in order:

1. **Format code**
   ```powershell
   uv run ruff format docling tests
   ```

2. **Lint and fix**
   ```powershell
   uv run ruff check --fix docling tests
   ```

3. **Type check**
   ```powershell
   uv run mypy docling
   ```

4. **Run tests**
   ```powershell
   uv run pytest
   ```

5. **Run pre-commit (optional, but recommended)**
   ```powershell
   uv run pre-commit run --all-files
   ```

## Utility Commands

### Check Python version
```powershell
python --version
# or
uv python list
```

### Check installed packages
```powershell
uv pip list
```

### Update dependencies
```powershell
uv sync --upgrade
```

### Clean build artifacts
```powershell
# Remove __pycache__ directories
Get-ChildItem -Recurse -Filter "__pycache__" | Remove-Item -Recurse -Force

# Remove .pyc files
Get-ChildItem -Recurse -Filter "*.pyc" | Remove-Item -Force
```

### Check project structure
```powershell
# Tree view (if tree command available)
tree /F

# Or use PowerShell
Get-ChildItem -Recurse -Directory | Select-Object FullName
```