# HW/ Agents Catalog

**Quick reference for hardware design and PCB analysis agents.**

---

## 🎯 Quick Start

### Available Agents (2)

HW/ currently contains **2 specialized agents** for hardware analysis and documentation:

1. **pcb-hardware-analyst**: PCB analysis and component extraction
2. **electronic-datasheet-writer**: Professional datasheet generation

**No orchestrator yet** - call agents individually based on your needs.

---

## 📋 Task → Agent Quick Reference

| Your Task | Call This Agent | Output |
|-----------|----------------|--------|
| **Analyze PCB design** | `pcb-hardware-analyst` | Component list, connections, analysis |
| **Generate component datasheet** | `electronic-datasheet-writer` | Professional datasheet PDF/markdown |

---

## 📦 Available Agents

### 1. pcb-hardware-analyst

**Purpose**: PCB schematic and layout analysis

**What it does**:
- Extracts component information (ICs, passives, connectors)
- Analyzes electrical connections and nets
- Identifies design patterns (power distribution, signal routing)
- Generates component Bill of Materials (BOM)

**Input**:
- PCB schematic files (KiCad, Altium, etc.)
- Layout files
- Component datasheets

**Output**:
- Component extraction report
- Connection analysis
- Design recommendations

**When to use**:
- Initial PCB design review
- Reverse engineering existing hardware
- BOM generation
- Design validation

**File**: `pcb-hardware-analyst.md`

---

### 2. electronic-datasheet-writer

**Purpose**: Professional electronic component datasheet generation

**What it does**:
- Creates structured datasheets from component specifications
- Formats technical specifications professionally
- Generates application notes and usage guidelines
- Produces pin diagrams and electrical characteristics tables

**Input**:
- Component specifications
- Electrical characteristics
- Application information
- Design considerations

**Output**:
- Professional datasheet (markdown or PDF)
- Formatted according to industry standards
- Ready for documentation or customer delivery

**When to use**:
- Documenting custom hardware modules
- Creating internal component documentation
- Generating customer-facing datasheets
- Standardizing component specifications

**File**: `electronics-datasheet-writer.md`

---

## 🔄 Common Workflow Patterns

### Pattern 1: PCB Documentation Workflow
```
1. pcb-hardware-analyst
   ↓
   [Analyze PCB, extract components]
   ↓
2. electronic-datasheet-writer
   ↓
   [Generate datasheets for custom components]
```

### Pattern 2: Reverse Engineering Workflow
```
1. pcb-hardware-analyst
   ↓
   [Extract component list and connections]
   ↓
   [Manual verification]
   ↓
2. electronic-datasheet-writer
   ↓
   [Document findings as datasheet]
```

---

## 🗺️ Data Flow

```
┌──────────────────────┐
│ pcb-hardware-analyst │
│ (PCB analysis)       │
└──────────┬───────────┘
           │
           ↓
    Component specifications
    BOM
    Connection analysis
           │
           ↓
┌──────────────────────────┐
│ electronic-datasheet-    │
│ writer                   │
│ (Documentation)          │
└──────────┬───────────────┘
           │
           ↓
    Professional datasheets
```

---

## 📁 Output Locations

Agents write to: **`project-context/HW/{project-name}/`**

```
project-context/
└── HW/
    └── your-hardware-project/
        ├── pcb_analysis.md           ← pcb-hardware-analyst
        ├── component_bom.md          ← pcb-hardware-analyst
        ├── datasheet_{component}.md  ← electronic-datasheet-writer
        └── _project_metadata.json    ← Tracking info
```

---

## 💡 Tips for Claude Code

### When to Use Each Agent

**Use pcb-hardware-analyst when**:
- User provides PCB files (schematic, layout)
- User asks to "analyze hardware", "extract components", "generate BOM"
- Reverse engineering task
- Design review needed

**Use electronic-datasheet-writer when**:
- User asks to "create datasheet", "document component"
- Professional documentation needed
- Component specifications provided
- Customer-facing documentation required

### Suggested Future: HW Orchestrator

As HW/ grows, consider creating `hw-workflow-orchestrator` to chain:
1. PCB analysis → 2. Component extraction → 3. Datasheet generation

---

## 🎓 Examples for Claude Code

### Example 1: User Provides PCB Schematic

**Your decision**:
```
User: "Analyze this KiCad PCB design"
  ↓
Read HW/agents/README.md
  ↓
Task = PCB analysis → pcb-hardware-analyst
  ↓
Call: /pcb-hardware-analyst with file path
```

### Example 2: User Wants Component Documentation

**Your decision**:
```
User: "Create a datasheet for my custom sensor module"
  ↓
Read HW/agents/README.md
  ↓
Task = datasheet generation → electronic-datasheet-writer
  ↓
Call: /electronic-datasheet-writer with specifications
```

---

## 🔗 Related Documentation

- **Individual agent details**: See `.md` files in this directory
- **Creating new HW agents**: See `../../meta-agent.md`
- **Atomic architecture**: See `../../README.md`

---

**Last Updated**: 2025-11-22
**Agent Count**: 2
**Category**: Hardware Design & Analysis
