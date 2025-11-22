# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository serves as a centralized collection of Claude AI agents for Nexilica. Each agent is specialized for specific tasks (Python development, C coding, VHDL, documentation analysis, etc.) and is designed to be used with Claude Code's agent system.

## Repository Architecture

### Core System File

**meta-agent.md**: Defines the meta-agent identity - an AI assistant specialized in creating AI agents for Claude. This file contains:
- The methodology for transforming user prompts into comprehensive agent descriptions
- **Agent Architecture Patterns**: When to create monolithic, atomic, or orchestrator agents
- **Project Context Integration**: How agents should read/write to project-context/
- **Templates**: Structured templates for atomic agents and orchestrators
- **References**: Examples from existing agents (SW/, HW/, FW/, Repo/)
- Output format requirements for Claude CLI agent generation workflow
- Integration with Claude's `/agents` → "generate with claude (recommended)" feature

### Agent Organization by Functional Category

Agents are organized into functional domains for atomic, composable workflows:

```
nexilica-agents/
├── FW/              # Firmware development agents
├── HW/              # Hardware design and analysis agents
├── SW/              # Software development agents (atomic workflow)
├── Repo/            # Repository management agents
└── General purpose/ # Cross-domain utility agents
```

**Atomic Workflow Philosophy**: Complex tasks are decomposed into specialized agents that work together through orchestration, improving speed and reducing context overload.

### Project Context System

All agents output to a centralized `project-context/` directory:

```
Workspace/
├── {project-name}/              # Project codebase (untouched)
└── project-context/             # Centralized agent outputs
    ├── SW/
    │   └── {project-name}/
    │       ├── context_snapshot.md      # Fast project overview
    │       ├── sw_context.md            # Detailed documentation
    │       ├── architecture_report.md   # Architectural analysis
    │       ├── test_report.md           # Code review findings
    │       └── _project_metadata.json   # Tracking metadata
    ├── HW/
    ├── FW/
    └── [other categories...]
```

**Benefits**:
- Separates generated documentation from source code
- Enables agent-to-agent data passing via standard files
- Maintains project history and analysis artifacts
- Supports multi-project workflows in single workspace

### Agent Structure Pattern

Each agent follows a consistent structure:

```
{category}/{agent-name}/
  agents/
    {agent-name}.md      # Agent configuration (YAML frontmatter + task description)
    README.md            # User guide with examples and best practices
```

**Agent Configuration File** (`{agent-name}.md`):
- YAML frontmatter: `name`, `description`, `tools`, `model`, `permissionMode`, `color`
- Task description with Core Workflow, Critical Rules, Example Interactions
- Project context management instructions (reading/writing to project-context/)
- Integration points with other agents

**README.md**:
- Usage instructions (direct invocation, automatic invocation, orchestration)
- Main functionality explanation
- Practical examples and scenarios
- Integration with other agents in the workflow
- Troubleshooting and customization guidance

### SW/ Category - Atomic Python Workflow

The SW/ category implements an atomic, orchestrated workflow for Python development:

**Atomic Agents** (6):
- **python-context-scanner**: Fast project scanning → context_snapshot.md
- **python-library-advisor**: Library selection with pros/cons
- **python-developer**: Pure code implementation (Python 3.10+)
- **python-documenter**: Documentation maintenance (sw_context.md)
- **python-tester**: Code review and test suggestions
- **python-architecture-analyst**: Deep architectural analysis

**Orchestrator** (1):
- **python-workflow-orchestrator**: Coordinates atomic agents into 5 predefined workflows (quick fix, new feature, analysis, refactoring, review)

**Performance**: 5-10x faster on large codebases by avoiding repeated full codebase reads. Agents share data via project-context/ files.

## Workflow for Creating New Agents

When asked to create a new agent:

1. **Read `meta-agent.md`** to understand the agent creation methodology and architectural patterns
2. **Determine functional category**: SW, HW, FW, Repo, or General purpose
3. **Follow established pattern** from existing agents in the same category
4. **Create directory structure**: `{category}/{agent-name}/agents/`
5. **Generate agent configuration file** with:
   - YAML frontmatter (name, description, tools, model, permissionMode, color)
   - Comprehensive task description with Core Workflow, Critical Rules
   - **Project context management** section (how to read/write project-context/ files)
   - Integration points with other agents in the workflow
6. **Generate user-facing README.md** with examples, usage patterns, and integration documentation
7. **If creating atomic workflow agents**:
   - Define clear input/output contracts (which files in project-context/)
   - Document data flow between agents
   - Update or create orchestrator agent if needed
8. **Update main README.md**: Add agent to appropriate category section with description and use cases
9. **Update CLAUDE.md**: Add to category's agent list if it's a new workflow pattern

## Key Concepts

**Agent Task Descriptions**: Must be formatted for Claude CLI's agent generation feature and compatible with the `/agents` workflow. They should be comprehensive enough for Claude to generate fully functional agent configurations.

**Documentation Philosophy**: Each agent should be self-documenting with clear workflows, rules, and examples to ensure consistent behavior across invocations.

**System.md Integration**: When creating agents, reference the official Claude documentation at https://platform.claude.com/docs/en/home and follow the structured output format defined in system.md.
