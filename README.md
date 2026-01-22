# Architecture Documentation Plugin

Generate technical architecture documentation from codebases with system diagrams, component analysis, and detailed engineering rationale.

## Features

- **C4 Model Diagrams**: System context, container, and component diagrams using Eraser syntax
- **Component Responsibility Matrix**: Quick-reference table of all components with responsibilities, dependencies, failure modes, and recovery strategies
- **Engineering Depth**: Configuration rationale, library choices, performance decisions with specific metrics
- **Optional Appendices**: Technology stack summary and API endpoint reference

## Installation

```bash
/plugin marketplace add dha201/architecture-documentation-plugin
/plugin install architecture-documentation
```

## Usage

Invoke the skill when you need architecture documentation:

```
@architecture-documentation Generate architecture documentation for this codebase
```

Or let Claude automatically detect when to use it based on your request for system design docs, technical handoffs, or architecture reviews.

## What It Generates

1. **Abstract** - Formal overview of system purpose and approach
2. **Context & Scope** - Business goals with system context diagram
3. **Architecture Constraints & Principles** - Design decisions and immutable rules
4. **High-Level Architecture** - Container diagram with data flow walkthrough
5. **Component Deep Dives** - Responsibility matrix + detailed analysis per component
6. **Cross-Cutting Concerns** - Observability, failure modes, deployment
7. **Decision Log** - ADRs with context and consequences
8. **Optional Appendices** - Tech stack summary and API reference

## Output Format

- Markdown document with embedded Eraser diagram code blocks
- Prose trade-offs analysis with specific metrics
- Configuration tables with rationale
- Concrete examples with code snippets and line numbers

## Requirements

- Claude Code 1.0.33 or later
- Codebase with dependency files (package.json, requirements.txt, etc.)

## License

MIT
