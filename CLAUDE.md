# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

A media collection — not a code project. It holds Anthropic research article PDFs alongside their AI-generated audio/video derivatives (Claude Code TTS narrations and NotebookLM discussions). There is no build system, no tests, no application code.

## Key Conventions

- **Source PDFs** go in `src_pdfs/`
- **Claude Code-generated audio** (MP3 via the `/audify` skill) goes in `claude_code_generated_audio/`
- **NotebookLM outputs** go in `notebookLM_outputs/notebookLM_audio/` (M4A) and `notebookLM_outputs/notebookLM_video/` (MP4)
- **All audio/video files are git-ignored** — they're too large for GitHub. They live on Google Drive and can be regenerated from the source PDFs.
- Only PDFs, markdown, and config files are tracked in git.

## Common Workflows

### Generate audio from a PDF
```bash
python3 ~/.claude/skills/audify/scripts/audify.py "src_pdfs/Article Name.pdf" -o short_name.mp3
```
Use `--dry-run` first for a cost estimate. Move the output MP3 to `claude_code_generated_audio/`.

### Upload and share media files
```bash
gws drive files create --json '{"name": "filename.mp3"}' --upload "/absolute/path/filename.mp3"
gws drive permissions create --params '{"fileId": "<ID>"}' --json '{"role": "reader", "type": "user", "emailAddress": "<email>"}'
```

## File Naming

- Claude audio: lowercase_snake_case derived from article title (e.g., `emotion_concepts_llm.mp3`)
- NotebookLM outputs: Title_Case_with_underscores as exported by NotebookLM
