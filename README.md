# Architecture Documentation Plugin

Three skills for technical documentation: architecture docs with C4 diagrams, technical debrief outlines, and a human writing style toolkit.

## Skills

### architecture-documentation

Generates architecture documentation from codebases with system diagrams, component analysis, and engineering rationale.

- C4 Model Diagrams (system context, container, component) using PlantUML/Kroki or Eraser syntax
- Component Responsibility Matrix with dependencies, failure modes, recovery strategies
- Configuration rationale, library choices, performance decisions with metrics
- Decision log (ADRs) with context and consequences
- Optional appendices: tech stack summary, API endpoint reference

### technical-debrief-outline

Creates structured presentation outlines for technical debriefs. Optimized for mixed audiences (engineers, PMs, executives).

- Problem-solution framing with real examples
- Mermaid diagrams for architecture sections
- Comparison tables (v1 vs v2, POC vs production)
- Presenter callout quotes and audience Q&A prep
- Includes a blank template in `references/outline_template.md`

### human-writing-style

Strips robotic AI patterns from any written content. Produces writing that sounds like a person wrote it.

- Banned word list (delve, leverage, robust, etc.)
- Short sentence / varied rhythm techniques
- Specificity over vagueness — numbers beat adjectives
- Coffee shop test: if it sounds like a LinkedIn post, rewrite it
- Works on docs, outlines, reports, changelogs, anything with words

## Installation

```bash
/plugin marketplace add dha201/architecture-documentation-plugin
/plugin install architecture-documentation
```

The marketplace will be registered as `dha201-plugins`.

## Usage

```
@architecture-documentation Generate architecture documentation for this codebase
@technical-debrief-outline Prepare a debrief for stakeholders
@human-writing-style Rewrite this to sound human
```

Or let Claude detect when to use them based on your request.

## Requirements

- Claude Code 1.0.33 or later

## License

MIT
