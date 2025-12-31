# StudyingPortal: Self-Hosted Local Course Loader & Progress Tracker

**StudyingPortal** is a sleek, self-hosted web app designed to load and view your offline video, audio, text, and quiz-based training courses. Whether it's Udemy downloads, "open sourced" training archives, or personal content, StudyingPortal turns your course folder into a fully navigable dashboard with automatic progress tracking.

---

## Features

* Dynamic folder parsing: Scans and maps your course structure into a browsable tree view.
* Video & Audio player: Integrated media player with resume & completion tracking.
* Text & HTML viewer: Supports .txt, .md, .html, .pdf, and more.
* Lesson progress tracking: Auto-saves your time spent and marks lessons as completed.
* Continue where you left off: Resume instantly from your last-accessed lesson.
* Local-first & private: 100% offline. No cloud, no tracking, no nonsense.
* Works with any course format: No metadata required, just structured folders.
* Ideal for hoarders, students, or offline learning setups

---

## Installation

### Quick Start (Local)

1. Clone the repo:

   ```bash
   git clone https://github.com/WhiskeyCoder/OfflineU.git
   cd OfflineU
   ```

2. Install Python dependencies:

   ```bash
   pip install flask
   ```

3. Run the app:

   ```bash
   python offlineu_core.py --create-templates
   ```

4. Open your browser:

   ```
   http://127.0.0.1:5000
   ```

---

## Folder Structure Example

```bash
MyCourse/
├── Section 1/
│   ├── 01 - Intro.mp4
│   ├── 02 - Setup Guide.pdf
│   └── 03 - Quiz.html
├── Section 2/
│   ├── 04 - Advanced Tips.mp4
│   └── resources/
│       └── extras.md
└── .studyingportal_progress.json  ← created automatically
```

> File types are detected automatically — videos, audio, quizzes, and docs.

---

## Supported File Types

| Type      | Extensions                                                  |
| --------- | ----------------------------------------------------------- |
| Videos    | `.mp4`, `.mkv`, `.webm`, `.mov`, `.avi`, etc.               |
| Audio     | `.mp3`, `.wav`, `.aac`, etc.                                |
| Docs      | `.txt`, `.md`, `.html`, `.pdf`, `.docx`                     |
| Subtitles | `.srt`, `.vtt`                                              |
| Quizzes   | Detected if file name contains `quiz`, `exam`, `test`, etc. |

---

## CLI Options

| Option               | Description                     |
| -------------------- | ------------------------------- |
| `--host`             | Set host (default: `127.0.0.1`) |
| `--port`             | Set port (default: `5000`)      |
| `--debug`            | Enable Flask debug mode         |
| `--create-templates` | Generate default HTML templates |
| `<course_path>`      | Load course directly at startup |

---

## Roadmap

* [x] Base function and testing
* [ ] Multi-user profile support
* [ ] Dark/light theme switcher
* [ ] Built-in quiz interactivity
* [ ] Import/export course metadata
* [ ] Mobile app wrapper
* [ ] Self hosted Docker Deployment

---

## Community

Join the development, suggest features, or ask questions via:

* GitHub Issues: [https://github.com/WhiskeyCoder/OfflineU/issues](https://github.com/WhiskeyCoder/OfflineU/issues)

---

## License

MIT License — Use freely, modify locally, share widely.

---

## Author

Built with ❤️ by [@WhiskeyCoder](https://github.com/WhiskeyCoder)
Inspired by the dream of **learning freely, offline, and without limits.**