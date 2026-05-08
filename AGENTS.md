# fastapi-utils: Agent Guidelines

Quick reference for contributors and AI agents working on this repository.

## Setup

**Install dependencies:**
```bash
python3 -m venv venv
source venv/bin/activate
pip install -e ".[all]"      # Full install with SQLAlchemy, pydantic-settings, typing-inspect
pip install -r requirements.txt  # Or use this for dev dependencies
```

**Verify environment:**
```bash
pytest -q      # Should pass all 72 tests
```

## Testing

**Run tests:**
```bash
pytest --cov=fastapi_utils              # With coverage
pytest -q                               # Quiet mode
make test                               # Makefile target
```

**Coverage reports:**
```bash
make testcov   # Generates htmlcov/index.html
```

Test files mirror module structure: `tests/test_*.py` for each `fastapi_utils/*.py` module.

## Style

**Auto-format code:**
```bash
black fastapi_utils tests               # Line length: 120
ruff check --fix fastapi_utils tests    # Auto-fix linter issues
```

**Check without fixing:**
```bash
black --check --diff fastapi_utils tests
ruff check fastapi_utils tests
make lint                               # Run both checks
```

## Review

**Type checking:**
```bash
mypy --show-error-codes fastapi_utils tests
make mypy
```

**Full validation (like CI):**
```bash
make static   # Runs: format lint mypy (must all pass)
make all      # Runs: static test (comprehensive check)
```

**Known warnings** (non-critical, documented):
- SQLAlchemy 2.0 deprecations in `tests/conftest.py` (lines 14, 38)
- Unregistered pytest marks in `tests/test_tasks.py` (timeout decorators)

## Key Project Details

- **Python:** 3.8+ (supports 3.8–3.12)
- **Framework:** FastAPI ≥0.89, Pydantic >1.0
- **Optional deps:** SQLAlchemy, pydantic-settings, typing-inspect
- **Main modules:** CBV, APIModel, APISettings, session management, timing, tasks
- **Test framework:** pytest with asyncio, coverage, timeout support
