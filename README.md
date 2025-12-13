# source-code-extractor

A small utility script that converts an entire source-code repository into a single text file.  
Useful when you want to provide a project snapshot to an LLM or perform full-text search over a codebase.

The script walks a directory, skips common noise (build artifacts, binaries, media files, etc.), detects binary-like content, and outputs clean text blocks:

    === FILE: src/app/main.cpp (size: 812 bytes) ===
    <file contents>

    === FILE: web/components/Button.jsx ===
    <file contents>

---

## Features

- Works with any language (Java, C/C++, Go, Rust, Python, JS/TS, etc.)
- Skips common build/cache directories  
- Filters out binary and media files automatically  
- Configurable ignore lists (directories, extensions, filenames)  
- Optional extension whitelist: include only `.py`, `.cpp`, `.java`, etc.  
- Adjustable max file size  
- Simple CLI interface

---

## Installation

Requires **Python 3.9+**.

Clone the repository:

    git clone https://github.com/shalchianmh/project-to-AI-context.git
    cd project-to-AI-context

Run:

    python source_code_extractor.py --help

---

## Usage

Basic usage:

    python source_code_extractor.py

Specify project folder and output file:

    python source_code_extractor.py \
        --project-dir /path/to/project \
        --output dump.txt

Limit max file size:

    python source_code_extractor.py --max-file-size 2MB

Ignore more directories:

    python source_code_extractor.py --ignore-dir coverage --ignore-dir logs

Ignore file extensions:

    python source_code_extractor.py --ignore-ext .log --ignore-ext .csv

Restrict to specific extensions (whitelist):

    python source_code_extractor.py --include-ext .py --include-ext .js

Follow symlinks:

    python source_code_extractor.py --follow-symlinks

---

## Output Format

Each included file becomes one block:

    === FILE: path/to/file.ext (size: N bytes) ===
    <contents>

Skipped files are also listed with their reason (binary-like, too large, ignored, error).

---

## Notes

- Use a whitelist (`--include-ext`) for very large monorepos.  
- Always review the dump before sharing; it may contain secrets.  
- Non-UTF-8 files are decoded best-effort with errors ignored.

---

## License

MIT License
