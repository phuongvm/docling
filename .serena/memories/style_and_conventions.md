# Docling: Code Style and Conventions

## Code Style Guidelines

### Formatting
- **Tool**: Ruff (formatter and linter)
- **Line Length**: 88 characters
- **Target Python Version**: 3.9+ (configured in pyproject.toml)

### Linting Rules (Ruff)
**Enabled Checks:**
- `C` - flake8-comprehensions
- `C9` - mccabe (complexity, max=30)
- `E` - pycodestyle errors
- `F` - pyflakes
- `I` - isort (import sorting)
- `PD` - pandas-vet
- `PIE` - pie
- `Q` - flake8-quotes
- `RUF` - All ruff-specific checks
- `S307` - eval usage
- `W` - pycodestyle warnings
- `ASYNC` - async checks
- `UP` - pyupgrade

**Ignored Checks:**
- `C408` - Unnecessary `dict()` call
- `E501` - Line too long (handled by formatter)
- `D107` - Missing docstring in `__init__`
- `F401` - Imported but unused
- `F811` - Redefinition
- `PL` - Pylint (disabled)
- `RUF012` - Mutable Class Attributes
- `UP006` - List vs list
- `UP007` - Option and Union
- `UP035` - `typing.Set` deprecated

### Import Sorting
- Uses `isort` via Ruff
- `combine-as-imports = true`
- Per-file ignores: `__init__.py` allows `E402`, `F401`

### Type Hints
- **Type Checker**: MyPy
- **Configuration**: `no_implicit_optional = true`
- **Pydantic Plugin**: Enabled for Pydantic model validation
- **Python Version**: 3.10 (for type checking)
- **Strict Mode**: Not enabled (relaxed for third-party libraries)

**MyPy Overrides:**
Many third-party modules are set to `ignore_missing_imports = true`:
- docling_parse.*, pypdfium2.*, networkx.*, scipy.*
- filetype.*, tesserocr.*, docling_ibm_models.*
- easyocr.*, ocrmac.*, onnxruntime.*
- mlx_vlm.*, lxml.*, huggingface_hub.*
- transformers.*, pylatexenc.*, vllm.*, qwen_vl_utils.*

### Naming Conventions
- Follow PEP 8 naming conventions
- Class names: PascalCase
- Function/variable names: snake_case
- Constants: UPPER_SNAKE_CASE

### Docstrings
- Docstrings are not strictly enforced (D107 ignored)
- Use standard Python docstring conventions when present

### Code Complexity
- Maximum complexity: 30 (McCabe)
- Configured in `[tool.ruff.lint.mccabe]`

### Test Code Style
- Tests in `tests/` directory
- ASYNC check disabled for test files: `"tests/*.py" = ["ASYNC"]`
- Test files follow pytest conventions

### Pre-commit Hooks
All style checks run automatically via pre-commit:
- Ruff formatter (auto-fixes formatting)
- Ruff linter (auto-fixes issues)
- MyPy type checking
- uv-lock validation

**Note**: Ruff checks will "fail" if they modify files. This is expected - you need to `git add` the modified files and commit again.

## File Organization

### Package Structure
- Main package: `docling/`
- Backends: `docling/backend/` (one file per format)
- CLI: `docling/cli/` (main.py for docling command, tools.py for docling-tools)
- Data models: `docling/datamodel/` (Pydantic models)
- Models: `docling/models/` (ML model implementations)
- Pipeline: `docling/pipeline/` (processing pipelines)
- Utils: `docling/utils/` (helper functions)

### Test Organization
- Tests mirror package structure
- Test data in `tests/data/` and `tests/data_scanned/`
- E2E tests: `test_e2e_conversion.py`, `test_e2e_ocr_conversion.py`
- Backend tests: `test_backend_*.py`
- CLI tests: `test_cli.py`

## Design Patterns

### Backend Pattern
- Abstract base class: `AbstractDocumentBackend`
- Each format has its own backend class
- Backends implement format-specific parsing logic

### Pipeline Pattern
- Processing pipelines for different workflows
- Pipeline options via Pydantic models
- Support for VLM, ASR, and standard pipelines

### Model Factory Pattern
- Model factories in `docling/models/factories/`
- Plugin system for model registration

## Git Conventions

### Commit Messages
Uses semantic release with Angular commit format:
- Allowed types: `build,chore,ci,docs,feat,fix,perf,style,refactor,test`
- Minor version bump: `feat`
- Patch version bump: `fix,perf`
- Version source: `tag_only`
- Branch: `main`