# AGENTS.md - StudyingPortal Development Guide

This file provides guidance for AI agents working on the StudyingPortal codebase.

## Build & Run Commands

### Running the Application
```bash
python offlineu_core.py                    # Default: 127.0.0.1:5000
python offlineu_core.py --host 0.0.0.0 --port 8080
python offlineu_core.py --debug             # Auto-reload + verbose errors
python offlineu_core.py /path/to/course     # Auto-load course
python offlineu_core.py --create-templates  # Regenerate HTML templates
```

### Docker Commands
```bash
docker build -t studyingportal .
docker-compose up
docker run -p 5000:5000 -v $(pwd)/courses:/app/courses studyingportal
```

### Testing
No test framework configured. Add pytest if creating tests.

### Linting & Type Checking
No tools configured. Consider: black (formatting), ruff/pylint (linting), mypy (type checking).

## Code Style Guidelines

### Python Code

#### Type Hints
Always use type hints. Import from `typing`: `List`, `Dict`, `Optional`, `Any`, `Tuple`.
Use `Optional[T]` for nullable values. Example: `def parse_course(path: str) -> Optional[Course]:`

#### Data Structures
Use `dataclass` for models (Lesson, DirectoryNode, Course). Initialize mutable defaults in `__post_init__`. Convert to dict with `asdict()`.

#### Imports
Order: standard library → third-party → local imports. One import per line. No blank lines between groups.
```python
import os
import json
from pathlib import Path
from typing import List, Dict, Optional, Any
from flask import Flask, render_template, jsonify
```

#### Naming Conventions
Variables/functions: snake_case (`load_progress`)
Classes: PascalCase (`DynamicCourseParser`)
Constants: UPPER_CASE (`VIDEO_EXTENSIONS`)
Private methods: prefix with `_` (`_build_directory_tree`)

#### Path Handling
Use `pathlib.Path` for all file operations. Normalize to forward slashes: `.replace('\\', '/')`
Validate paths are within course directory: `if not full_path.startswith(course_path): return "Access denied", 403`

#### Error Handling
Use specific exceptions: `(PermissionError, OSError)`. Catch broad exceptions as last resort.
Print errors to console, return user-friendly messages in API responses. Return appropriate HTTP codes: 400, 403, 500.

#### String Formatting & Comments
Use f-strings. Avoid `%` formatting. Minimize comments - code should be self-documenting. Use docstrings for public APIs.

### Flask Patterns

Use `@app.route` decorators. Return HTML with `render_template()`, JSON with `jsonify()`. Use `redirect()` and `url_for()` for navigation.
Access global state (e.g., `current_course`) only within route handlers. Validate all user input. Use `SECRET_KEY` for sessions.

### HTML & Jinja2 Templates

Use `{{ variable }}` for output, `{% control %}` for logic. Embed CSS in `<style>` tags, JavaScript in `<script>` tags.
Styling: Dark theme (bg `#1a1a1a`, surface `#2d2d2d`, primary `#007acc`). Use flexbox and media queries for responsiveness.

### File Operations

Use `mimetypes.guess_type()` for MIME types. Serve files with `send_file()`. Always validate paths before serving.
Store progress as JSON in `.offlineu_progress.json` with `indent=2`. Include: completed, progress_seconds, last_accessed.

### Constants

Define at module level:
- `VIDEO_EXTENSIONS`: video formats
- `AUDIO_EXTENSIONS`: audio formats
- `SUBTITLE_EXTENSIONS`: subtitle formats
- `TEXT_EXTENSIONS`: document formats
- `QUIZ_INDICATORS`: keywords to detect quizzes

### General Guidelines

- Group functionality in classes (DynamicCourseParser, ProgressTracker)
- Use static methods for stateless utilities
- Keep route handlers in main module
- Separate parsing, progress tracking, and API concerns
- Use `argparse` for CLI with help text
- Support environment variables (e.g., `AUTO_LOAD_COURSE`)
- Handle both Windows and Unix systems with `platform.system()`
- Normalize paths to forward slashes for web serving
- Handle permission errors gracefully
- JSON-based file storage only (no SQL database)
- Single user local app (no authentication)

### Running Single Test
No test framework currently. If adding pytest: `pytest tests/test_module.py::test_function`