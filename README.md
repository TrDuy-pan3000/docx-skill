# docx-skill

> **An AI Agent Skill for reading, editing, and formatting `.docx` files** via direct OOXML manipulation — no Word installation required.

---

## Table of Contents

- [What this skill does](#what-this-skill-does)
- [Skill entry point](#skill-entry-point)
- [Repository structure](#repository-structure)
- [Quickstart](#quickstart)
  - [1. Unpack a `.docx` for editing](#1-unpack-a-docx-for-editing)
  - [2. Edit the document (Python)](#2-edit-the-document-python)
  - [3. Repack into `.docx`](#3-repack-into-docx)
  - [4. Create a new document from scratch (JavaScript)](#4-create-a-new-document-from-scratch-javascript)
- [Key workflows](#key-workflows)
- [Academic formatting support](#academic-formatting-support)
- [Dependencies](#dependencies)
- [License](#license)

---

## What this skill does

This skill gives an AI agent the ability to:

- **Read & analyze** any `.docx` file (text extraction, structure inspection)
- **Edit existing documents** — formatting, tracked changes (redlining), captions, tables, styles
- **Create new documents** from scratch using `docx-js`
- **Apply academic/professional formatting** standards (Vietnamese university standards supported)
- **Auto-generate front matter** — Table of Contents, List of Figures, List of Tables, Abbreviations

---

## Skill entry point

[`SKILL.md`](SKILL.md) — the AI reads this file to understand the full workflow decision tree.

---

## Repository structure

```
docx-skill/
├── SKILL.md                  # ← AI skill instruction file (entry point)
├── ooxml.md                  # OOXML/Python Document library reference (~600 lines)
├── docx-js.md                # docx-js JavaScript library reference (~500 lines)
│
├── ooxml/
│   ├── scripts/
│   │   ├── unpack.py         # Unzip .docx → editable directory
│   │   ├── pack.py           # Repack directory → .docx
│   │   └── validate.py       # Validate OOXML schema compliance
│   └── schemas/              # OOXML XSD schema references
│
└── scripts/
    ├── __init__.py
    ├── document.py           # Core Document library (OOXML manipulation API)
    ├── utilities.py          # Helper utilities (XML, formatting, sections)
    └── templates/            # XML fragment templates
```

---

## Quickstart

### 1. Unpack a `.docx` for editing
```bash
python ooxml/scripts/unpack.py MyDocument.docx unpacked/
```

### 2. Edit the document (Python)
```python
import sys
sys.path.insert(0, "scripts")
from document import Document

doc = Document("unpacked/word/document.xml")
# ... make changes using the Document API (see ooxml.md)
doc.save()
```

### 3. Repack into `.docx`
```bash
python ooxml/scripts/pack.py unpacked/ MyDocument_edited.docx
```

### 4. Create a new document from scratch (JavaScript)
```bash
# See docx-js.md for full API reference
node create_document.js
```

---

## Key workflows

| Task | Tool | Reference |
|---|---|---|
| Read/extract text | `pandoc` | `SKILL.md` → Text extraction |
| Inspect raw XML | `unpack.py` | `SKILL.md` → Raw XML access |
| Edit formatting, styles | `document.py` | `ooxml.md` → Document Library |
| Tracked changes (redlining) | `document.py` | `SKILL.md` → Redlining workflow |
| Create new document | `docx-js` | `docx-js.md` |
| Apply academic formatting | `document.py` | `ooxml.md` → Formatting patterns |

---

## Academic formatting support

The skill supports Vietnamese university thesis/report formatting standards:

- **Paper**: A4 Portrait, Times New Roman 13pt, 1.2 line spacing
- **Margins**: Top/Bottom 2.5cm, Left 3cm, Right 2cm
- **Captions**: `Hình X.Y: Name` (below figures), `Bảng X.Y: Name` (above tables)
- **Page numbering**: Roman numerals for front matter, Arabic from Chapter 1
- **Auto-generated**: TOC, List of Figures, List of Tables, Abbreviations

---

## Dependencies

```bash
# Python (for OOXML editing)
pip install defusedxml

# Text extraction
# macOS: brew install pandoc
# Ubuntu: sudo apt-get install pandoc

# New document creation (JavaScript)
npm install -g docx

# PDF/Image conversion (optional)
# Ubuntu: sudo apt-get install libreoffice poppler-utils
```

---

## License

[MIT License](LICENSE.txt) — Copyright (c) 2026 TrDuy-pan3000
