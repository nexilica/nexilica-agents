# Python Project Analyzer Agent - User Guide

## Files Created

- `python-project-analyzer.md` - Complete agent configuration

## How to Use the Agent

### Method 1: Direct Invocation

You can invoke the agent directly in your Claude Code conversations using:

```
/python-project-analyzer
```

This will activate the specialized agent that follows all defined rules.

### Method 2: Automatic Invocation

Claude Code can automatically invoke this agent when you:
- Ask to understand how a Python codebase works
- Request documentation of project structure
- Need comprehensive analysis of a Python project
- Want to prepare documentation for another AI agent
- Provide a directory path containing Python files for analysis

### Method 3: Generation with Claude (Recommended for Customizations)

If you want to modify or regenerate the agent:

1. Run `/agents` in Claude Code
2. Select "generate with claude (recommended)"
3. Describe the modifications you want
4. Claude will generate a new version

## Main Functionality

### 1. Comprehensive Code Analysis

Systematic examination of Python codebases:
- Analyzes all .py files in the project directory
- Identifies all Python modules and libraries used
- Consults official Python documentation for accurate understanding
- Analyzes code architecture, design patterns, and implementation
- Identifies project type (headless, GUI, or hybrid)
- Understands data flow, class hierarchies, and module dependencies

### 2. Project Type Detection

Automatically identifies:
- **Headless Scripts**: Command-line utilities, batch processors, APIs
- **GUI Applications**: tkinter, PyQt, Kivy, or other GUI frameworks
- **Hybrid Projects**: Combined CLI and GUI capabilities
- **Web Applications**: Flask, Django, FastAPI frameworks
- **Data Science**: Jupyter notebooks, pandas/numpy pipelines

### 3. Documentation Generation

Creates `software_report.md` with:
- Project overview and purpose
- Main features and capabilities
- Technical architecture explanation
- Key modules and dependencies
- Data flow and logic descriptions
- Project structure tree
- File descriptions
- Technical notes and recommendations

### 4. AI-Optimized Format

Report designed for:
- Human developers understanding the codebase
- AI agents performing code improvements
- Team onboarding and knowledge transfer
- Code review and documentation purposes

## Software Report Structure

The generated `software_report.md` includes:

```markdown
# Software Report: [Project Name]

## Overview
[Brief description of software purpose and main functionality]

## Software Functionality

### Main Features
[Clear description of primary features]

### Technical Architecture
- Type: [Headless/GUI/Hybrid/Web]
- Main Entry Point: [Entry file and function]
- Core Components: [Key modules and roles]

### Key Modules and Dependencies
[List of Python modules with explanations]
- `module_name`: [Purpose in this project]

### Data Flow and Logic
[How data moves through the system]

### GUI Framework (if applicable)
[Details about GUI implementation]

## Project Structure
```
[ASCII tree representation]
```

### File Descriptions
[What each significant file does]

## Technical Notes
[Important technical considerations]

## Recommendations for Improvement
[Optional: Enhancement opportunities]
```

## Example Usage Scenarios

### Example 1: New Project Analysis

```
User: Can you analyze the Python project in ./my_app and create documentation?

Agent: I'll analyze your project systematically...

[Agent performs]:
- Scans all .py files in ./my_app
- Identifies Flask web framework and SQLAlchemy
- Consults official documentation for Flask and SQLAlchemy
- Analyzes route definitions and database models
- Maps data flow from endpoints to database
- Generates comprehensive software_report.md

Result: Complete documentation explaining the web application architecture
```

### Example 2: Understanding Before Modifications

```
User: I need to understand what this Python codebase does before making changes

Agent: Let me examine the codebase and provide a clear explanation...

[Agent analyzes]:
- Entry point: main.py
- Type: GUI application using tkinter
- Core modules: ui_manager.py, data_processor.py, file_handler.py
- Data flow: User input → Processing → File export
- Dependencies: pandas, openpyxl, tkinter

[Generates report with]:
- High-level functionality overview
- Module-by-module breakdown
- Data processing pipeline explanation
- GUI layout and interaction patterns
```

### Example 3: Documentation for AI Improvement

```
User: Here's my Python project folder - I need documentation that another AI can use to improve the code

Agent: I'll create detailed software_report.md optimized for AI agent consumption...

[Report includes]:
- Precise technical architecture
- Module coupling and dependencies
- Code conventions and patterns used
- Areas requiring careful modification
- Current implementation details
- Potential improvement opportunities
```

### Example 4: Italian Project

```
User: Analizza questo progetto Python e crea la documentazione

Agent: Analizzerò il progetto Python e genererò un report completo...

[Agent adapts to Italian context]:
- Recognizes Italian comments and docstrings
- Provides technical report in clear language
- Maintains technical terminology standards
```

## Key Features

### ✅ Systematic Analysis
Examines every Python file to ensure complete understanding of the codebase.

### ✅ Documentation Research
Consults official Python documentation for each module to ensure accuracy.

### ✅ Project Structure Visualization
Creates clear ASCII tree diagrams showing directory hierarchy.

### ✅ Type Detection
Automatically identifies whether project is headless, GUI, web, or hybrid.

### ✅ Dependency Mapping
Lists all external libraries and explains their role in the project.

### ✅ Data Flow Analysis
Traces how data moves through the system from input to output.

### ✅ AI-Optimized Output
Report format designed for consumption by AI agents performing code improvements.

### ✅ Bilingual Support
Recognizes and adapts to Italian or English contexts.

## Agent Rules

The agent follows these core principles:

1. ✅ **Complete File Scan**: Examines all .py files in the project directory
2. ✅ **Documentation Verification**: Consults official Python docs for accurate module understanding
3. ✅ **Clear Structure**: Uses ASCII tree diagrams for project visualization
4. ✅ **Precise Explanations**: Provides concise but complete technical descriptions
5. ✅ **AI-Friendly Format**: Includes sufficient context for AI agent consumption
6. ✅ **No Assumptions**: Notes limitations when files or components cannot be accessed
7. ✅ **Context Awareness**: Recognizes and adapts to Italian/English environments

## Operational Guidelines

### Clarity Over Verbosity
- Keeps explanations concise but complete
- Avoids unnecessary jargon
- Maintains technical accuracy

### Structure Visualization
- Uses ASCII tree diagrams with proper indentation
- Shows clear hierarchy and relationships
- Annotates directories with descriptions

### Module Documentation
For each significant module:
- Purpose and responsibility
- Key functions and classes
- External dependencies
- Role in overall architecture

### Error Handling
If encountering issues:
- Notes files that cannot be accessed
- Documents limitations in understanding
- Suggests what additional information would help

## Best Practices

### When to Invoke the Agent

- Before modifying unfamiliar Python codebases
- When preparing project documentation
- For team knowledge transfer
- Before AI-assisted code improvements
- During code reviews
- For project handoff to other developers

### Preparing Your Project

**Optimal Setup:**
```
✅ All Python files organized in logical structure
✅ Clear entry point (main.py, app.py, etc.)
✅ Requirements.txt or setup.py present
✅ README or docstrings providing context
```

**Minimum Requirements:**
```
✅ At least one Python file to analyze
✅ Directory path accessible
```

### Communicating with the Agent

**Clear and Specific:**
```
✅ "Analyze the Python project in ./src and create documentation"
✅ "I need to understand how this Flask application works"
✅ "Create a software report for this data processing script"
```

**To Avoid:**
```
❌ "Look at this code" (without specifying directory)
❌ "Analyze everything" (too vague)
```

**Effective Requests:**
```
✅ "Analyze the Python project in ./my_app and explain its architecture"
✅ "I need documentation for this codebase that another AI can use for improvements"
✅ "Create a comprehensive report of this GUI application"
```

## Analysis Process

The agent follows this workflow:

1. **Scan Project**: Identify all .py files in directory tree
2. **Parse Structure**: Build project structure tree
3. **Identify Entry Point**: Find main execution entry (main.py, __main__ blocks)
4. **Analyze Dependencies**: Extract all imported modules
5. **Research Modules**: Consult official documentation for libraries
6. **Type Detection**: Determine if headless, GUI, web, or hybrid
7. **Data Flow Analysis**: Trace data movement through system
8. **Generate Report**: Create comprehensive software_report.md
9. **Quality Check**: Verify completeness and accuracy

## Quality Assurance

Before finalizing the report, the agent verifies:
- ✅ All major Python files analyzed
- ✅ Project structure tree is accurate and complete
- ✅ Module dependencies correctly identified
- ✅ Functionality description is clear and accurate
- ✅ Report provides sufficient context for code improvement
- ✅ Entry points and execution flow documented

## Troubleshooting

### Agent doesn't activate automatically

- Use direct invocation: `/python-project-analyzer`
- Verify the file is in `.claude/agents/`

### Incomplete analysis

**Check project structure:**
```
✅ All Python files have .py extension
✅ Directory path is correct and accessible
✅ Project has identifiable structure
```

### Missing module information

- The agent will note when modules are unrecognized
- Consult requirements.txt for complete dependency list
- Check if using custom/internal modules

### Report lacks specific details

- Ensure Python files have clear structure
- Add docstrings and comments for better understanding
- Verify entry points are clearly defined

### AI agent can't use report effectively

- Ensure report includes:
  - ✅ Precise technical architecture
  - ✅ Module coupling information
  - ✅ Code conventions used
  - ✅ Areas requiring careful modification

## Integration with Other Agents

This agent works well with:
- **python-specialist**: Use analyzer first, then specialist for improvements
- Other code improvement agents: Report provides necessary context
- Documentation agents: Analyzer output can feed documentation generation

**Workflow:**
```
1. python-project-analyzer creates software_report.md
2. Another agent reads software_report.md for context
3. Improvement agent makes informed changes based on report
```

## Customization

To modify the agent behavior:

1. Open `.claude/agents/python-project-analyzer.md`
2. Modify the YAML frontmatter to change:
   - `model`: Model to use (sonnet, opus, haiku)
3. Modify the markdown content to change:
   - Analysis depth and focus
   - Report structure and sections
   - Specific aspects to emphasize
   - Additional quality checks

## Support

For issues or questions:
- Consult official documentation: https://code.claude.com/docs/en/sub-agents.md
- Use `/help` in Claude Code
- Ask Claude Code directly about the agent's behavior

---

**Agent Version**: 1.0
**Model**: Sonnet
**Languages Supported**: Italian, English
**Created**: 2025-11-21
