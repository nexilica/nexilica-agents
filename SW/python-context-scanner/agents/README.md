# Python Context Scanner Agent

Fast Python project scanner that generates lightweight context snapshots without deep analysis.

## Purpose

This agent is the **foundation** of the Python workflow system. It quickly scans Python projects and creates structured snapshots that other specialized agents use as input, eliminating the need for expensive repeated file reads.

## Key Features

- ✅ **Lightning Fast**: Scans 100-file projects in 10-20 seconds
- ✅ **Centralized Context**: Outputs to `project-context/SW/{project}/`
- ✅ **Auto-Detection**: Finds or creates project-context/ automatically
- ✅ **Smart Caching**: Skips re-scan if no files changed
- ✅ **Metadata Tracking**: Maintains `_project_metadata.json` with project info
- ✅ **Framework Detection**: Identifies Flask, FastAPI, PyQt, tkinter, etc.
- ✅ **Dependency Extraction**: Captures requirements and imports
- ✅ **Configurable**: Supports custom context path via `.claude/config.json`

## Usage

### Direct Invocation

```bash
/python-context-scanner
```

### Automatic Invocation

The `python-workflow-orchestrator` automatically calls this agent as the first step of any Python workflow.

### When to Use Directly

- You want a quick overview of a Python project
- Before starting development on existing code
- To generate context for other agents to consume
- After major structural changes to refresh the snapshot

## Output Location

```
your-workspace/
├── my-python-project/          ← Your code (untouched)
│   └── [Python files...]
└── project-context/            ← Generated context
    └── SW/
        └── my-python-project/
            ├── context_snapshot.md      ← Main output
            └── _project_metadata.json   ← Tracking metadata
```

## What It Does

### Quick Discovery
1. Finds all Python files using glob patterns
2. Generates ASCII directory tree
3. Extracts all import statements
4. Identifies entry points (`if __name__ == "__main__"`)
5. Counts files and lines of code

### Lightweight Analysis
1. Categorizes files (modules, scripts, tests, config)
2. Detects frameworks (web, GUI, database, etc.)
3. Extracts top-level class and function names (no deep reading)
4. Parses requirements.txt or pyproject.toml

### Snapshot Generation
Creates structured markdown with:
- Project statistics
- Directory structure with descriptions
- Key components and entry points
- Dependencies (standard library + external)
- Detected frameworks
- Important classes/functions (top-level only)
- Code organization patterns

## What It Doesn't Do

- ❌ Deep code analysis (use `python-architecture-analyst` for that)
- ❌ Code execution or testing
- ❌ Detailed function-by-function breakdown
- ❌ Performance profiling
- ❌ Security auditing

## Performance Targets

| Project Size | Expected Time |
|--------------|---------------|
| <20 files | 3-5 seconds |
| 20-100 files | 8-15 seconds |
| 100-500 files | 20-40 seconds |
| >500 files | 60-90 seconds |

## Configuration

### Default Behavior
Scans for `project-context/` in parent directory of project. Creates if missing.

### Custom Path
Create `.claude/config.json` in project root:
```json
{
  "project_context_root": "/custom/path/to/contexts"
}
```

## Example Output

**context_snapshot.md** excerpt:
```markdown
# Context Snapshot: Flask API Server

**Generated**: 2025-11-22T02:30:00Z
**Project Path**: /home/user/projects/flask-api

## Quick Stats
- **Total Files**: 23
- **Total Lines**: 1847
- **Main Entry**: app.py:42
- **Project Type**: Web Application

## Dependencies
flask==3.0.0
sqlalchemy==2.0.23
pydantic==2.5.0

## Detected Frameworks
- **Web**: Flask 3.0
- **Database**: SQLAlchemy ORM
```

## Integration with Other Agents

This agent's output is consumed by:
- **python-developer**: Understands existing code structure
- **python-architecture-analyst**: Starting point for deep analysis
- **python-library-advisor**: Reviews current dependencies
- **python-documenter**: References for documentation updates
- **python-tester**: Identifies test coverage needs
- **python-workflow-orchestrator**: Decides workflow based on snapshot

## Caching Behavior

**Smart Re-scan Detection**:
- Checks file modification times before scanning
- If no .py files changed since last scan, reuses existing snapshot
- Updates only metadata timestamp
- Saves 10-60 seconds on unchanged projects

**Force Re-scan**:
Explicitly request if needed: "Re-scan the project completely"

## Troubleshooting

### Issue: "Cannot find project root"
**Solution**: Run from within your Python project directory

### Issue: "Permission denied creating project-context/"
**Solution**: Check write permissions in parent directory, or use custom path via config

### Issue: "Scan taking too long (>2 minutes)"
**Solution**: Project may be very large. Agent will prompt for sampling strategy.

### Issue: "Missing dependencies in snapshot"
**Solution**: Ensure `requirements.txt` or `pyproject.toml` exists, or dependencies will be inferred from imports

## Best Practices

1. **Run first**: Always run this agent before other Python agents on new projects
2. **Keep current**: Re-run after major structural changes (new directories, renamed files)
3. **Review snapshot**: Check the generated markdown to verify accuracy
4. **Configure once**: Set custom context path if working across multiple workspaces

## Examples

### Example 1: First-time Project Analysis
```
User: "I need to understand this Python codebase"
Assistant: [Calls python-context-scanner]
Output: context_snapshot.md with full overview in 12 seconds
User can now ask questions based on clear structure
```

### Example 2: Before Development
```
User: "Add authentication to my Flask app"
Orchestrator: [Calls python-context-scanner first]
Context captured in 8 seconds
Developer agent reads snapshot, implements auth without re-reading all files
```

### Example 3: Large Codebase
```
User: "Scan my 800-file Django project"
Scanner: Detects large project, completes in 75 seconds
Generates comprehensive snapshot
Other agents work from snapshot (fast) instead of reading 800 files (slow)
```

---

**Related Agents**:
- [python-architecture-analyst](../../python-architecture-analyst/agents/README.md) - Deep analysis
- [python-developer](../../python-developer/agents/README.md) - Code development
- [python-workflow-orchestrator](../../python-workflow-orchestrator/agents/README.md) - Workflow coordination
