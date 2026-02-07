---
name: rendering-docx
description: Use when architecture documentation needs to be delivered as a Word document, stakeholders request formal .docx artifacts instead of markdown, or compliance/audit requires rendered diagrams embedded in Word format
---

# Rendering Architecture Docs to DOCX

Converts architecture markdown with diagram code blocks into a polished Word document. Diagrams render via Kroki API and embed as PNG images. Supports any Kroki-supported diagram type (PlantUML, C4, Mermaid, D2, Graphviz, etc.).

## Workflow

Copy this checklist and track progress:

```
- [ ] Step 1: Verify dependencies installed
- [ ] Step 2: Run the render script
- [ ] Step 3: Verify output
- [ ] Step 4: Deliver to user
```

**Step 1: Verify dependencies**

```bash
pip install -r scripts/requirements.txt
```

Requires: `python-docx>=1.1.0`, `requests>=2.31.0`, `mistune>=3.0.0`, `Pillow>=10.0.0`

**Step 2: Run the render script**

```bash
python scripts/render-docx.py <input.md> [-o output.docx]
```

| Option | Description | Default |
|--------|-------------|---------|
| `-o, --output` | Output DOCX path | `<input>.docx` |
| `--kroki-url` | Kroki instance URL | `https://kroki.io` |
| `--image-width` | Max image width (inches) | `6.0` |
| `--template` | Corporate `.dotx` template | None |

**Step 3: Verify output**

Open the generated DOCX and check:
- Diagrams rendered as images (not raw code)
- Tables have blue header rows (not plain text)
- Headings appear in navigation pane
- Right-click TOC → Update Field → Update Entire Table

**Step 4: Deliver**

Report the output path and file size to the user. Note that TOC requires manual update in Word.

## Error Recovery

If the script fails:

1. **Kroki render error** — The failing diagram type and error are printed. Check the diagram syntax. C4 diagrams must have `!include <C4/...>` or use the `c4plantuml` fence tag — otherwise they route to the wrong Kroki endpoint.
2. **Network error** — Kroki.io may be rate-limited. Self-host: `docker run -p8000:8000 yuzutech/kroki` and pass `--kroki-url http://localhost:8000`.
3. **Missing tables in output** — The script enables mistune's table plugin automatically. If tables still appear as text, the markdown pipe table syntax may be malformed (check alignment row `|---|---|`).

## Key Behaviors

**C4 routing:** Diagrams with C4 markers (`!include <C4/...>`, `C4_Context`, `C4_Container`) route to `/c4plantuml/png`, not `/plantuml/png`. Tag fence blocks `c4plantuml` to force this.

**Untagged PlantUML:** Code blocks without a fence tag but containing `@startuml` are auto-detected.

**Figure captions** follow this priority:

| Priority | Source | Example |
|----------|--------|---------|
| 1 | HTML comment `<!-- caption: ... -->` | `<!-- caption: System Context -->` |
| 2 | PlantUML name `@startuml Name` | `@startuml System Context` |
| 3 | Preceding heading | `### System Architecture` |
| 4 | Fallback | `Diagram 1`, `Diagram 2`, ... |

**Page breaks:** `---` (thematic break) in markdown inserts a page break in the DOCX.

**Document structure:** Title page (from first H1) → Table of Contents → Body with headings, formatted text, rendered diagrams, tables, lists, block quotes, and code blocks.

**Template support:** Pass `--template corporate.dotx` to apply corporate styles. The script adds Figure Caption and Code Block styles only if absent from the template.

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| C4 diagram renders incorrectly | Ensure `!include <C4/...>` is present or tag as `c4plantuml` |
| Images too wide/small | Adjust `--image-width` (default 6.0 inches) |
| TOC is empty in Word | Right-click TOC → Update Field → Update Entire Table |
| Kroki rate limited | Self-host with Docker and use `--kroki-url` |
