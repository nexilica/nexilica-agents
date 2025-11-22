# SW/ Agents Catalog

**Quick reference for Python software development atomic agents.**

This catalog helps Claude Code (and you) quickly identify which agent to use for specific tasks.

---

## 🎯 Quick Start

### For Most Tasks (Recommended)
**Use**: `/python-workflow-orchestrator`

The orchestrator automatically:
- Detects your task type (bug fix, new feature, analysis, refactoring, review)
- Chains the right atomic agents in sequence
- Handles user interaction (library selection, approvals)
- Consolidates results into clear summary

**Simply describe what you want**, and it handles the rest.

### For Specific Needs
Call individual atomic agents directly when you need granular control (see table below).

---

## 📋 Task → Agent Quick Reference

| Your Task | Call This Agent | Duration | Output |
|-----------|----------------|----------|--------|
| **Quick project scan** | `python-context-scanner` | 10-20 sec | context_snapshot.md |
| **Get library recommendations** | `python-library-advisor` | 15-30 sec | Library proposals |
| **Implement code changes** | `python-developer` | 30-120 sec | Modified .py files |
| **Update project docs** | `python-documenter` | 10-30 sec | sw_context.md |
| **Review code quality** | `python-tester` | 30-90 sec | test_report.md |
| **Analyze architecture** | `python-architecture-analyst` | 2-5 min | architecture_report.md |
| **Complete workflow** | `python-workflow-orchestrator` | 1-5 min | All of the above |

---

## 📦 Available Agents

### 🎭 Orchestrator (Recommended Entry Point)

**python-workflow-orchestrator**
- **Purpose**: Master coordinator for Python development
- **What it does**: Automatically detects task type and chains appropriate atomic agents
- **Workflows**: 5 predefined (quick fix, new feature, analysis, refactoring, review)
- **When to use**: 95% of the time - handles everything automatically
- **File**: `python-workflow-orchestrator.md`

---

### ⚛️ Atomic Agents (Granular Control)

**1. python-context-scanner**
- **Purpose**: Fast project scanning and structure extraction
- **Input**: Project directory path
- **Output**: `context_snapshot.md` (structure, dependencies, entry points, frameworks)
- **Duration**: 10-20 seconds (100 files), up to 90 sec (500+ files)
- **When to use**: First step of any workflow, or when context is stale
- **Key feature**: Smart caching (skips re-scan if no files changed)
- **File**: `python-context-scanner.md`

**2. python-library-advisor**
- **Purpose**: Library selection with pros/cons analysis
- **Input**: Requirement description + context_snapshot.md
- **Output**: 2-4 library options with recommendations
- **Duration**: 15-30 seconds
- **When to use**: When you need to choose a library but aren't sure which
- **Key feature**: Never makes decisions for you - always presents options
- **File**: `python-library-advisor.md`

**3. python-developer**
- **Purpose**: Pure code implementation (Python 3.10+)
- **Input**: Task description + context_snapshot.md + library choice
- **Output**: Modified Python files
- **Duration**: 30-120 seconds
- **When to use**: For actual code writing/modification
- **Key feature**: Uses context_snapshot instead of reading full codebase (5-10x faster)
- **Focus**: Implementation only - no docs, no testing
- **File**: `python-developer.md`

**4. python-documenter**
- **Purpose**: Documentation maintenance for sw_context.md
- **Input**: Code changes description + file list
- **Output**: Updated `sw_context.md` with change log
- **Duration**: 10-30 seconds
- **When to use**: After any code changes to keep docs current
- **Key feature**: Works from diffs, not full codebase re-reads
- **File**: `python-documenter.md`

**5. python-tester**
- **Purpose**: Code quality review and test suggestions
- **Input**: Modified files list
- **Output**: `test_report.md` (issues found, test suggestions)
- **Duration**: 30-90 seconds
- **When to use**: Before committing, merging, or deploying
- **Key feature**: Runs static analysis (mypy, ruff) if available
- **File**: `python-tester.md`

**6. python-architecture-analyst**
- **Purpose**: Deep architectural analysis and recommendations
- **Input**: context_snapshot.md or full project
- **Output**: `architecture_report.md` (design patterns, bottlenecks, recommendations)
- **Duration**: 2-5 minutes
- **When to use**: Initial project analysis, refactoring planning, technical debt assessment
- **Key feature**: Strategic insights with prioritized recommendations (P1/P2/P3)
- **File**: `python-architecture-analyst.md`

---

## 🔄 Common Workflow Patterns

### Workflow A: Quick Bug Fix (1-2 min)
```
python-workflow-orchestrator
    ↓
python-context-scanner (10-20 sec)
    ↓
python-developer (30-60 sec)
    ↓
python-documenter (15 sec)
```

### Workflow B: New Feature with Library Selection (2-5 min)
```
python-workflow-orchestrator
    ↓
python-context-scanner (10-20 sec)
    ↓
python-library-advisor (20 sec)
    ↓
[USER CHOOSES LIBRARY]
    ↓
python-developer (1-2 min)
    ↓
python-documenter (20 sec)
    ↓
python-tester (30-60 sec)
```

### Workflow C: Project Understanding (1-3 min)
```
python-workflow-orchestrator
    ↓
python-context-scanner (10-20 sec)
    ↓
python-architecture-analyst (1-3 min)
```

### Workflow D: Major Refactoring (5-10 min)
```
python-workflow-orchestrator
    ↓
python-context-scanner (10-20 sec)
    ↓
python-architecture-analyst (2-3 min)
    ↓
[USER REVIEWS RECOMMENDATIONS]
    ↓
python-developer (2-5 min)
    ↓
python-documenter (30 sec)
    ↓
python-tester (1-2 min)
```

### Workflow E: Quality Review (1-2 min)
```
python-workflow-orchestrator
    ↓
python-context-scanner (10-20 sec)
    ↓
python-tester (1-2 min)
```

---

## 🗺️ Data Flow Between Agents

```
┌─────────────────────┐
│ python-context-     │
│ scanner             │
└──────────┬──────────┘
           │
           ↓
    context_snapshot.md ←──────────┐
           │                       │
           ├───────────────────────┤
           │                       │
           ↓                       ↓
┌──────────────────┐    ┌────────────────────┐
│ python-library-  │    │ python-            │
│ advisor          │    │ architecture-      │
└────────┬─────────┘    │ analyst            │
         │              └─────────┬──────────┘
         ↓                        │
    [USER CHOICE]                 ↓
         │              architecture_report.md
         ↓
┌──────────────────┐
│ python-developer │
└────────┬─────────┘
         │
         ↓
    [CODE CHANGES]
         │
    ┌────┴─────┐
    │          │
    ↓          ↓
┌──────────┐ ┌──────────┐
│ python-  │ │ python-  │
│ documen- │ │ tester   │
│ ter      │ │          │
└────┬─────┘ └────┬─────┘
     │            │
     ↓            ↓
sw_context.md  test_report.md
```

**Key insight**: `context_snapshot.md` is cached and shared by all agents → 80% faster on repeated operations.

---

## 📁 Output Locations

All agents write to: **`project-context/SW/{project-name}/`**

```
project-context/
└── SW/
    └── your-project/
        ├── context_snapshot.md      ← python-context-scanner
        ├── sw_context.md            ← python-documenter
        ├── architecture_report.md   ← python-architecture-analyst
        ├── test_report.md           ← python-tester
        └── _project_metadata.json   ← All agents (tracking)
```

**Why separate from code?**
- Keeps source code clean
- Enables agent-to-agent data passing
- Maintains analysis history
- Supports multi-project workflows

---

## ⚡ Performance Characteristics

| Project Size | Context Scanner | Full Workflow (Orchestrator) |
|--------------|-----------------|------------------------------|
| Small (<20 files) | 3-5 sec | 1-2 min |
| Medium (20-100 files) | 8-15 sec | 2-4 min |
| Large (100-500 files) | 20-40 sec | 3-6 min |
| Very Large (>500 files) | 60-90 sec | 5-10 min |

**Comparison to monolithic approach**:
- **5-10x faster** on large codebases
- **70% less context tokens** used
- **90% fewer timeouts** (no more "Claude is taking too long")
- **Significantly better output quality** due to specialized prompts

---

## 💡 Tips for Claude Code

### When to Call Orchestrator vs Atomic Agents

**Use orchestrator when**:
- User request is high-level ("add feature", "fix bug", "analyze project")
- Multiple steps are needed
- You're not sure which agents to chain

**Call atomic agents directly when**:
- User specifically asks for one thing ("scan the project", "review this code")
- You need granular control over workflow
- You're building a custom workflow

### Optimization Strategies

1. **Check for cached context**: If `context_snapshot.md` exists and is recent (<10 min), skip scanner
2. **Read catalog first**: This file (you're reading it now!) tells you exactly which agent to use
3. **Parallel execution**: When possible, run documenter + tester in parallel after development
4. **User interaction**: Always wait for user input when library-advisor presents options

### Error Handling

- **Missing context_snapshot.md**: Call python-context-scanner first
- **Agent timeout**: Project may be too large - suggest sampling or directory filtering
- **Library not specified**: Call python-library-advisor to present options

---

## 🎓 Examples for Claude Code

### Example 1: User Says "Add Flask authentication"

**Your decision process**:
1. Read this catalog → See orchestrator handles "add feature" tasks
2. Call: `/python-workflow-orchestrator` with user request
3. Let orchestrator handle the workflow (it will chain scanner → advisor → developer → documenter → tester)

### Example 2: User Says "Quickly scan this Python project"

**Your decision process**:
1. Read this catalog → "Quick project scan" = python-context-scanner
2. Call: `/python-context-scanner` directly
3. Return context_snapshot.md location to user

### Example 3: User Says "What libraries can I use for HTTP requests?"

**Your decision process**:
1. Read this catalog → Library questions = python-library-advisor
2. First check if context_snapshot.md exists (for context)
   - If not: call python-context-scanner first
3. Call: `/python-library-advisor` with requirement
4. Present options to user

### Example 4: User Says "Review the code I just wrote"

**Your decision process**:
1. Read this catalog → Code review = python-tester
2. Get list of modified files (git diff or user specification)
3. Call: `/python-tester` with file list
4. Present test_report.md findings

---

## 🔗 Related Documentation

- **Individual agent details**: See each `.md` file in this directory
- **Agent creation guide**: See `../../meta-agent.md` for creating new agents
- **Atomic architecture theory**: See `../../README.md` for full explanation
- **Project context system**: See `../../CLAUDE.md` for architecture details

---

**Last Updated**: 2025-11-22
**Agent Count**: 7 (6 atomic + 1 orchestrator)
**Category**: Software Development (Python)
