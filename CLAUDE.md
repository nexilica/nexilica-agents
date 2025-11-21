# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository serves as a centralized collection of Claude AI agents for Nexilica. Each agent is specialized for specific tasks (Python development, C coding, VHDL, documentation analysis, etc.) and is designed to be used with Claude Code's agent system.

## Repository Architecture

### Core System File

**system.md**: Defines the meta-agent identity - an AI assistant specialized in creating AI agents for Claude. This file contains:
- The methodology for transforming user prompts into comprehensive agent descriptions
- Output format requirements for Claude CLI agent generation workflow
- Integration with Claude's `/agents` → "generate with claude (recommended)" feature

### Agent Structure Pattern

Each agent follows a consistent structure in its own directory:

```
{agent-name}/
  agents/
    {agent-name}.md      # Agent configuration (YAML frontmatter + task description)
    README.md            # User guide with examples and best practices
```

**Agent Configuration File** (`{agent-name}.md`):
- YAML frontmatter: `name`, `description`, `tools`, `model`, `permissionMode`
- Task description with Core Workflow, Critical Rules, Example Interactions
- Structured guidelines specific to the agent's domain

**README.md**:
- Usage instructions (direct invocation, automatic invocation, generation)
- Main functionality explanation
- Practical examples and scenarios
- Troubleshooting and customization guidance

### Existing Agents

- **python-specialist**: Python 3.10+ development with automatic `sw_context.md` documentation maintenance, library proposal workflow, and GUI/scripting specialization

## Workflow for Creating New Agents

When asked to create a new agent:

1. Read `system.md` to understand the agent creation methodology
2. Follow the established pattern from existing agents (e.g., `python-specialist/`)
3. Create directory structure: `{agent-name}/agents/`
4. Generate agent configuration file with YAML + comprehensive task description
5. Generate user-facing README.md with examples and usage patterns
6. Ensure the agent's workflow includes proper tool usage and critical rules
7. **Update the main README.md**: Add the new agent to the "Agents Disponibili" section with complete description, characteristics, and use cases

## Key Concepts

**Agent Task Descriptions**: Must be formatted for Claude CLI's agent generation feature and compatible with the `/agents` workflow. They should be comprehensive enough for Claude to generate fully functional agent configurations.

**Documentation Philosophy**: Each agent should be self-documenting with clear workflows, rules, and examples to ensure consistent behavior across invocations.

**System.md Integration**: When creating agents, reference the official Claude documentation at https://platform.claude.com/docs/en/home and follow the structured output format defined in system.md.
