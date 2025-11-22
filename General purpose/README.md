# General Purpose/ Agents Catalog

**Quick reference for cross-domain utility and validation agents.**

---

## 🎯 Quick Start

### Available Agents (1)

General purpose/ currently contains **1 specialized agent** for documentation validation:

**context-validator**: Expert documentation quality assurance specialist that validates markdown docs against canonical context (CLAUDE.md)

**No orchestrator needed** - these agents are standalone utilities that can be used across all categories (SW, HW, FW, Repo).

---

## 📋 Task → Agent Quick Reference

| Your Task | Call This Agent | Output |
|-----------|----------------|--------|
| **Validate documentation** | `context-validator` | Validation report with findings |
| **Check technical accuracy** | `context-validator` | Error list with corrections |
| **Verify guideline compliance** | `context-validator` | Compliance issues + fixes |
| **Quality assurance review** | `context-validator` | Comprehensive QA report |

---

## 📦 Available Agent

### context-validator

**Purpose**: Documentation quality assurance and validation against canonical context

**What it does**:
- Validates markdown documentation against CLAUDE.md (canonical project context)
- Checks technical accuracy (product specs, protocols, hardware details)
- Verifies guideline compliance (naming conventions, report standards)
- Identifies inconsistencies and contradictions
- Provides specific corrections with CLAUDE.md references
- Generates structured validation reports with prioritized findings

**Input**:
- Target markdown document(s) to validate
- CLAUDE.md (canonical context) - automatically located
- Optional: Specific validation focus areas

**Output**:
- Comprehensive validation report (markdown)
  - **Critical Issues** (must fix): Technical errors, spec violations
  - **Medium Priority** (should fix): Guideline non-compliance, naming issues
  - **Low Priority** (nice to fix): Style improvements, enhancements
- Each finding includes:
  - Issue description
  - Location in document
  - Severity level
  - Suggested correction
  - CLAUDE.md reference

**When to use**:
- After generating new reports or documentation
- Before sharing documents with stakeholders
- To verify existing documentation accuracy
- When updating product specifications
- For periodic quality assurance reviews
- To identify outdated or incorrect information
- When suspecting inconsistencies with CLAUDE.md

**Critical validations performed**:
- ✅ Technical specifications (sensor types, microcontrollers, protocols)
- ✅ Product description rules (context enforcement)
- ✅ Repository names and GitHub URLs
- ✅ Contributor name mappings
- ✅ Domain-specific terminology
- ✅ Cross-references and links
- ✅ Consistency with established patterns

**Typical findings**:
- Incorrect technical specifications
- Generic descriptions violating context guidelines
- Wrong repository names or URLs
- Incorrect contributor attributions
- Missing domain-specific context
- Speculation about unauthorized applications

**File**: `context-validator.md`

---

## 🔄 Common Workflow Patterns

### Pattern 1: Post-Generation Validation
```
[Generate documentation via any agent]
    ↓
context-validator
    ↓
Validation report with issues
    ↓
[Fix critical and medium issues]
    ↓
[Optional: Re-validate]
```

### Pattern 2: Batch Validation
```
context-validator (doc 1)
    ↓
context-validator (doc 2)
    ↓
context-validator (doc 3)
    ↓
Consolidated validation report
```

### Pattern 3: Pre-Delivery QA
```
[Documentation ready]
    ↓
context-validator
    ↓
Review findings
    ↓
Fix critical issues
    ↓
[Deliver to stakeholders]
```

### Future Pattern: Automated Documentation Pipeline
```
[When more General purpose agents exist]

doc-generator
    ↓
context-validator (QA)
    ↓
doc-formatter (standardization)
    ↓
doc-publisher (distribution)
```

---

## 📁 Output Locations

Agent writes to: **`project-context/General purpose/{project-name}/`**

```
project-context/
└── General purpose/
    └── validated-project/
        ├── validation_report.md      ← context-validator
        ├── critical_issues.md        ← context-validator (filtered)
        └── _project_metadata.json    ← Tracking info
```

---

## 💡 Tips for Claude Code

### When to Use context-validator

**Use when**:
- User generates documentation (reports, READMEs, datasheets)
- User asks to "validate documentation", "check for errors"
- User requests "quality assurance", "review accuracy"
- Before finalizing documents for stakeholders
- After updating technical specifications
- User suspects inconsistencies

### Validation Scope

The validator checks against **CLAUDE.md** which typically contains:
- Product naming conventions
- Technical specifications (hardware, firmware, software)
- Repository information and URLs
- Contributor name mappings
- Domain-specific guidelines
- Approved terminology
- Context enforcement rules

### Priority Levels Explained

**🔴 Critical** (Must Fix Before Delivery):
- Technical specification errors
- Security vulnerabilities in docs
- Wrong repository or project names
- Incorrect component specifications
- Compliance violations

**🟡 Medium** (Should Fix Soon):
- Missing type hints or incomplete sections
- Incomplete error handling documentation
- Code quality documentation issues
- Non-critical naming inconsistencies

**🟢 Low** (Nice to Have):
- Style improvements
- Minor refactoring suggestions
- Documentation enhancements
- Non-critical optimizations

### Integration with Other Categories

context-validator can validate documentation generated by:
- **SW/**: python-documenter output (sw_context.md)
- **HW/**: electronic-datasheet-writer output
- **FW/**: stm32-firmware-analyzer output (firmware_analysis.md)
- **Repo/**: github-extractor output (analysis reports)

### Future Expansion Suggestions

Consider adding to General purpose/:
1. **doc-formatter**: Standardize markdown formatting across all docs
2. **doc-generator**: Template-based documentation generation
3. **doc-translator**: Multi-language documentation support
4. **doc-linker**: Automatic cross-reference and link validation
5. **doc-publisher**: Convert markdown to PDF, HTML, Wiki formats

---

## 🎓 Examples for Claude Code

### Example 1: User Generated a Report

**Your decision**:
```
User: "Validate the report I just generated"
  ↓
Read General purpose/agents/README.md
  ↓
Task = documentation validation → context-validator
  ↓
Call: /context-validator with report path
  ↓
Return validation report with prioritized findings
```

### Example 2: Pre-Delivery QA Check

**Your decision**:
```
User: "Check if this datasheet is ready to send to the customer"
  ↓
Read General purpose/agents/README.md
  ↓
Task = quality assurance → context-validator
  ↓
Call: /context-validator with datasheet path
  ↓
If critical issues found: "Fix these first before delivery"
If no critical issues: "Ready for delivery (see minor suggestions)"
```

### Example 3: Batch Validation

**Your decision**:
```
User: "Validate all markdown files in /docs"
  ↓
Read General purpose/agents/README.md
  ↓
Task = batch validation → context-validator (multiple calls)
  ↓
For each .md file in /docs:
  Call: /context-validator
  ↓
Consolidate results into summary report
```

---

## 🔗 Related Documentation

- **Agent details**: See `context-validator.md` in this directory
- **Creating new utility agents**: See `../../meta-agent.md`
- **Atomic architecture**: See `../../README.md`
- **CLAUDE.md**: The canonical context file used for validation

---

**Last Updated**: 2025-11-22
**Agent Count**: 1
**Category**: General Purpose / Utilities
**Domain**: Documentation Quality Assurance
