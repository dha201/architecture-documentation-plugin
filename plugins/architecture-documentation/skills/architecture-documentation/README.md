# Architecture Documentation Skill

Generate comprehensive technical architecture documentation from codebases with embedded diagrams.

## Overview

This skill helps Claude Code analyze a codebase and produce in-depth technical documentation suitable for:
- **Engineers:** Implementation details, algorithms, failure handling
- **Architects:** System design, component interactions, trade-offs
- **Stakeholders:** High-level context, business goals
- **PMs:** System capabilities, constraints, decisions

**Focus:** Depth over breadth. Documents the "why" behind technical decisions, not just the "what."

## Quick Start

### 1. Generate Documentation

```bash
# In Claude Code, provide your codebase and invoke the skill:
# "Generate architecture documentation for this codebase"
```

Claude will:
1. Explore the codebase structure
2. Identify components and dependencies
3. Trace data flow through the system
4. Generate comprehensive documentation with diagrams
5. Output a markdown file with Eraser diagram code embedded

### 2. Render Diagrams

After Claude generates the documentation:

```bash
# Navigate to the skill directory
cd ~/.claude/skills/superpowers/architecture-documentation

# Render diagrams (requires Eraser API key)
./render-eraser-diagrams.js path/to/Architecture.md --format svg --replace

# Or just extract diagram code without rendering
./render-eraser-diagrams.js path/to/Architecture.md
```

## Documentation Template

The generated documentation follows this structure:

```
1. Context & Scope
   - Business goals
   - System context diagram

2. Architecture Constraints & Principles
   - Why this approach?
   - Immutable rules

3. High-Level Architecture
   - Container diagram
   - Data flow walkthrough with transformations

4. Component Deep Dives (for each component)
   - Purpose
   - Implementation details (stack, algorithms, dependencies)
   - Engineering analysis (trade-offs, configuration rationale, edge cases)
   - Component diagram

5. Cross-Cutting Concerns
   - Observability
   - Failure modes
   - Deployment

6. Decision Log
   - Major decisions with context and consequences
```

## Eraser Diagram Syntax

Claude generates diagrams using Eraser's diagram-as-code syntax:

```
// System Context Example
Users [icon: users]
API [icon: server]
Database [icon: database]

Users > API: HTTPS
API > Database: SQL

// Container Diagram
Frontend [icon: react] {
  label: "React SPA"
}
Backend [icon: nodejs] {
  label: "FastAPI"
}

Frontend > Backend: REST API

// Sequence Diagram
User > Frontend: Click button
Frontend > Backend: POST /api/data
Backend > Database: INSERT
Database > Backend: Success
Backend > Frontend: 200 OK
Frontend > User: Show success
```

## Eraser API Script

### Installation

```bash
# Install Node.js if not already installed
# Script requires Node.js 12+

# Set your Eraser API key
export ERASER_API_KEY="your-api-key-here"
```

### Usage

```bash
# Render all diagrams in a markdown file
./render-eraser-diagrams.js Architecture.md

# Specify output directory and format
./render-eraser-diagrams.js Architecture.md --output-dir ./images --format svg

# Replace diagram code blocks with image references
./render-eraser-diagrams.js Architecture.md --replace

# Full example
./render-eraser-diagrams.js Architecture.md \
  --output-dir ./diagrams \
  --format svg \
  --replace \
  --api-key "your-key"
```

### Options

| Option | Description | Default |
|--------|-------------|---------|
| `--output-dir <dir>` | Output directory for diagrams | `./diagrams` |
| `--format <format>` | Output format: `svg` or `png` | `svg` |
| `--replace` | Replace code blocks with image refs | `false` |
| `--api-key <key>` | Eraser API key (or use env var) | `ERASER_API_KEY` |

### Without API Key

If you don't have an Eraser API key, the script will extract diagram code to `.eraser` files:

```bash
./render-eraser-diagrams.js Architecture.md
# Creates: diagrams/system-context.eraser, diagrams/data-flow.eraser, etc.
```

You can then:
1. Visit https://app.eraser.io
2. Create a new diagram
3. Paste the `.eraser` file content
4. Export as image

## Reference Materials

This skill includes comprehensive reference materials to help Claude generate accurate documentation:

### 1. **example-output.pdf**
Gold standard example showing the expected documentation quality and structure. Based on a real AI Support Agents architecture.

### 2. **eraser-syntax.md**
Complete syntax reference for Eraser diagrams including:
- Node and group definitions
- All available properties (icon, color, label, shape, etc.)
- Connection types and labels
- Layout direction controls
- Common patterns and troubleshooting

### 3. **icon-reference.md**
Comprehensive icon catalog with 1600+ icons:
- 700+ AWS icons (EC2, Lambda, RDS, S3, etc.)
- 500+ GCP icons (Compute Engine, BigQuery, Pub/Sub, etc.)
- 400+ Azure icons (Virtual Machines, Cosmos DB, AKS, etc.)
- Kubernetes icons (Pod, Service, Deployment, etc.)
- Popular tech logos (Docker, React, Python, Postgres, etc.)
- General purpose icons (users, servers, databases, etc.)

### 4. **diagram-examples.md**
Real-world diagram examples with complete code:
- AWS three-tier web application
- Microservices architecture
- Data ETL pipeline
- Kubernetes cluster
- Serverless event-driven architecture
- Multi-region high availability
- CI/CD pipeline

Claude references these materials when generating documentation to ensure accuracy.

Key features:
- **Detailed transformations:** Shows exact input → output at each stage
- **Library rationale:** Documents WHY each dependency was chosen
- **Configuration explanations:** Explains WHY specific values are set
- **Trade-off analysis:** Discusses alternatives and why they were rejected
- **Failure handling:** Documents edge cases, retries, fallbacks
- **Concrete examples:** Real payloads, actual code snippets

## Customization

### Modifying the Template

Edit `SKILL.md` to adjust the documentation structure. The skill follows the template structure exactly.

### Adding Diagram Types

Eraser supports multiple diagram types:
- **Architecture diagrams:** System context, container, component
- **Sequence diagrams:** Request/response flows
- **Entity relationship:** Database schemas
- **Cloud architecture:** AWS/Azure/GCP resources

Refer to Eraser documentation for complete syntax: https://docs.eraser.io

### Adapting for Other Projects

This skill is codebase-agnostic and works with:
- **Backend services:** Node.js, Python, Go, Java, etc.
- **Frontend apps:** React, Vue, Angular
- **Full-stack applications**
- **Microservices architectures**
- **Monolithic applications**

The skill infers structure from common patterns (package.json, requirements.txt, go.mod, etc.).

## Tips for Best Results

1. **Provide context:** Include README, business requirements, or design docs in the codebase
2. **Point to entry points:** Mention main files (e.g., "main.py is the entry point")
3. **Highlight complexity:** Tell Claude which components are most complex
4. **Request specific focus:** "Focus on the authentication flow" or "Deep dive on the data processing pipeline"
5. **Iterate:** Review generated docs and ask Claude to expand specific sections

## Troubleshooting

### "No Eraser diagrams found"

The markdown file doesn't contain diagram code blocks. Make sure Claude generated the documentation with diagrams.

### "API request failed"

- Check your Eraser API key is valid
- Verify you have internet connectivity
- Ensure you haven't exceeded API rate limits

### "Diagram code is invalid"

- The generated diagram syntax may have errors
- Review the Eraser syntax documentation
- Ask Claude to regenerate the diagram

### Script won't run

```bash
# Make sure the script is executable
chmod +x render-eraser-diagrams.js

# Verify Node.js is installed
node --version  # Should be 12+
```

## API Key Setup

### Getting an Eraser API Key

1. Visit https://eraser.io
2. Sign up or log in
3. Go to Settings → API Keys
4. Create a new API key
5. Copy the key

### Setting the API Key

**Option 1: Environment Variable (Recommended)**
```bash
# Add to ~/.bashrc or ~/.zshrc
export ERASER_API_KEY="your-api-key-here"

# Or set for current session only
export ERASER_API_KEY="your-api-key-here"
```

**Option 2: Command Line Flag**
```bash
./render-eraser-diagrams.js Architecture.md --api-key "your-api-key-here"
```

## Architecture Decision

This skill prioritizes **depth for engineers** because:

1. **Translation is easier:** Engineers can simplify technical docs for stakeholders, but stakeholders can't add missing technical depth
2. **Structured review:** Technical documentation enables proper code review and architecture validation
3. **Onboarding:** New engineers need deep technical context to contribute effectively
4. **Maintenance:** Future modifications require understanding the "why" behind decisions

High-level summaries can be generated from detailed docs, but the reverse is not possible.

## License

This skill is part of the Superpowers skill collection.

## Contributing

To improve this skill:
1. Test with various codebases
2. Identify missing or unclear sections
3. Refine the template structure
4. Add examples and anti-patterns
5. Submit improvements to the Superpowers repository
