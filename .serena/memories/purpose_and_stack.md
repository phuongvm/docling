# Docling Project: Purpose and Tech Stack

## Project Purpose

Docling is a Python SDK and CLI tool for document processing and conversion. It parses diverse document formats (PDF, DOCX, PPTX, XLSX, HTML, audio, images, etc.) and converts them to a unified document representation format optimized for generative AI applications.

**Key Use Cases:**
- Document conversion for RAG (Retrieval Augmented Generation) pipelines
- Advanced PDF understanding (layout, tables, code, formulas)
- OCR processing for scanned documents
- Audio transcription with ASR models
- Integration with AI frameworks (LangChain, LlamaIndex, Crew AI, Haystack)
- MCP server for agentic AI applications

## Tech Stack

### Core Technologies
- **Language**: Python 3.9 - 3.14
- **Package Manager**: [uv](https://docs.astral.sh/uv/) (modern Python package manager)
- **Type System**: Pydantic v2 for data validation
- **CLI Framework**: Typer (built on Click)

### Development Tools
- **Linter & Formatter**: Ruff (replaces Black, isort, flake8)
- **Type Checker**: MyPy (with Pydantic plugin)
- **Testing**: pytest with coverage
- **Pre-commit**: Automated code quality checks
- **Documentation**: MkDocs with Material theme

### Key Dependencies
- `docling-core[chunking]` - Core document processing
- `docling-parse` - PDF parsing engine
- `docling-ibm-models` - IBM models for layout/OCR
- `pypdfium2` - PDF rendering
- `pydantic` - Data validation
- `huggingface_hub` - Model management
- `transformers` - ML models (optional, for VLM)
- `rapidocr` - OCR engine
- Various format backends (python-docx, python-pptx, openpyxl, etc.)

### Optional Dependencies
- `easyocr` - Alternative OCR
- `tesserocr` - Tesseract OCR binding
- `vlm` - Visual Language Models (transformers, mlx-vlm, vllm)
- `asr` - Automatic Speech Recognition (mlx-whisper, openai-whisper)

## Project Structure

```
docling/
├── docling/              # Main package
│   ├── backend/          # Format-specific backends (PDF, DOCX, HTML, etc.)
│   ├── cli/              # CLI entry points (main.py, tools.py)
│   ├── datamodel/        # Data models and configuration
│   ├── models/           # ML models (OCR, layout, VLM, ASR)
│   ├── pipeline/         # Processing pipelines
│   └── utils/            # Utility functions
├── tests/                # Test suite
├── docs/                 # Documentation (MkDocs)
└── pyproject.toml        # Project configuration
```

## Version

Current version: **2.66.0** (auto-updated, do not edit manually)

## License

MIT License