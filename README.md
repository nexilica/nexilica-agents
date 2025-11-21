# Nexilica Agents Repository

Centralized repository for all Claude AI agents used across Nexilica projects. Each agent is specialized for specific tasks and can be easily imported into other projects.

## How to Import an Agent into a Project

### Method 1: Manual Copy (Recommended)

1. Navigate to the agent folder you're interested in (e.g., `python-specialist/`)
2. Copy the `.md` file from the `agents/` subfolder
3. In your project, create the `.claude/agents/` directory if it doesn't exist
4. Paste the agent file into `.claude/agents/`
5. The agent will be automatically available in Claude Code

```bash
# Example for importing python-specialist
cp python-specialist/agents/python-specialist.md /path/to/your/project/.claude/agents/
```

### Method 2: Symlink (For Local Projects)

```bash
# Create a symbolic link to keep the agent always updated
ln -s /path/to/nexilica-agents/python-specialist/agents/python-specialist.md /path/to/your/project/.claude/agents/
```

### Method 3: Git Submodule (For Teams)

```bash
# Add this repo as a submodule
cd /path/to/your/project
git submodule add <repo-url> .agents-library

# Copy the necessary agents
cp .agents-library/python-specialist/agents/python-specialist.md .claude/agents/
```

### Verify Import

After importing, verify the agent is available:
1. Open Claude Code in your project
2. Type `/` to see the command list
3. The agent should appear as `/python-specialist` (or the imported agent name)

---

## Available Agents

### 🐍 Python Specialist

**File**: `python-specialist/agents/python-specialist.md`
**Invocation**: `/python-specialist`

**Description**:
Agent specialized in Python 3.10+ development with focus on GUI applications and scripting. Automatically maintains project documentation in a `sw_context.md` file.

**Key Features**:
- ✅ **Automatic Documentation**: Creates and maintains `sw_context.md` with project structure, functionality, implementation details, and change log
- ✅ **Intelligent Library Proposals**: When you don't specify a library, stops and proposes 2-4 options with pros/cons
- ✅ **Exclusive Library Usage**: When you specify a library, uses it directly without proposing alternatives
- ✅ **Automatic Contextualization**: On first use, reads all existing Python code and documents it
- ✅ **Python 3.10+ Only**: Uses match/case, union types, structural pattern matching

**When to Use**:
- GUI application development (tkinter, PyQt6, CustomTkinter)
- Python script creation
- Data analysis and manipulation
- Projects requiring automatic and detailed documentation
- When you want guidance in library selection

**Tools**: Read, Write, Edit, Grep, Glob, Bash
**Model**: Sonnet
**Permissions**: acceptEdits

**Full Documentation**: [python-specialist/agents/README.md](python-specialist/agents/README.md)

---

## Repository Structure

```
nexilica-agents/
├── README.md                    # This file
├── CLAUDE.md                    # Guide for Claude Code
├── system.md                    # Meta-agent for creating new agents
├── python-specialist/
│   └── agents/
│       ├── python-specialist.md # Agent configuration
│       └── README.md            # Detailed user guide
└── [other-agents]/              # Other specialized agents
    └── agents/
        ├── [agent-name].md
        └── README.md
```

---

## How to Contribute a New Agent

1. **Use the meta-agent**: The `system.md` file defines a meta-agent that creates other agents
2. **Follow the structure**: Each agent must have:
   - Directory `{agent-name}/agents/`
   - File `{agent-name}.md` with YAML frontmatter and task description
   - File `README.md` with user guide and examples
3. **Update this README**: Add the new agent to the "Available Agents" section
4. **Test the agent**: Verify it works correctly in a real project

---

## Support and Documentation

- **Claude Documentation**: https://code.claude.com/docs/en/sub-agents.md
- **Official Documentation**: https://platform.claude.com/docs/en/home
- **Claude Code Help**: Use `/help` in Claude Code for assistance

---

**Last Update**: 2025-11-21
**Number of Agents**: 1
