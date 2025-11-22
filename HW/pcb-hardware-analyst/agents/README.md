# PCB Hardware Analyst Agent - User Guide

## Files Created

- `pcb-hardware-analyst.md` - Complete agent configuration

## How to Use the Agent

### Method 1: Direct Invocation

You can invoke the agent directly in your Claude Code conversations using:

```
/pcb-hardware-analyst
```

This will activate the specialized agent that follows all defined rules.

### Method 2: Automatic Invocation

Claude Code can automatically invoke this agent when you:
- Mention PCB design analysis
- Have BOM (Bill of Materials) files in Export/BOM folder
- Have schematic PDFs in Export/Documentation folder
- Request hardware documentation
- Need component analysis and datasheet research
- Ask about PCB architecture or signal flow

### Method 3: Generation with Claude (Recommended for Customizations)

If you want to modify or regenerate the agent:

1. Run `/agents` in Claude Code
2. Select "generate with claude (recommended)"
3. Describe the modifications you want
4. Claude will generate a new version

## Main Functionality

### 1. BOM Analysis

Comprehensive examination of Bill of Materials:
- Extracts all component information
- Identifies part numbers and manufacturers
- Categorizes components by function
- Creates structured component summaries

### 2. Datasheet Research

Automatic datasheet retrieval and analysis:
- Searches online for official component datasheets
- Extracts key specifications from datasheets
- Identifies electrical characteristics
- Documents communication interfaces (I2C, SPI, UART, CAN)
- Notes absolute maximum ratings and operating conditions

### 3. Schematic Interpretation

Deep analysis of PCB schematics:
- **Power Architecture**: Maps voltage rails, regulators, power distribution
- **Signal Flow**: Traces critical signals through the system
- **Communication Buses**: Documents I2C, SPI, UART, CAN interfaces with addresses and configurations
- **Component Interconnections**: Shows how components interface with each other
- **Clock Domains**: Identifies clock sources and frequencies
- **Analog Sections**: Analyzes signal chains, filtering, and conditioning

### 4. System Architecture Documentation

Creates comprehensive technical reports:
- High-level system overview
- Functional block descriptions
- Component interactions and data flow
- Interface specifications
- Power distribution analysis

### 5. Hardware Report Generation

Generates `hardware_report.md` with complete documentation:
- Executive summary
- System architecture
- Component-by-component analysis
- Communication interface mappings
- Power distribution details
- Functional descriptions
- Component summary tables

## Critical File Handling Requirements

### ✅ ONLY Analyzes Files In:
- `Export/BOM/` folder - Bill of Materials files
- `Export/Documentation/` folder - Schematic PDFs and documentation

### ❌ NEVER Reads:
- KiCad files (.kicad_pcb, .kicad_sch, .kicad_pro)
- Eagle files (.brd, .sch)
- Altium files (.PcbDoc, .SchDoc)
- Any native CAD formats

This restriction ensures:
- Compatibility across different PCB design tools
- Works with exported documentation that's universally readable
- No dependency on specific CAD software versions

## Example Usage Scenarios

### Example 1: New Sensor Board Analysis

```
User: I've uploaded the files for our new sensor board. Can you analyze the design and create documentation?

Agent: I'll analyze your BOM and schematics from the Export folders...

[Agent performs]:
- Reads BOM files in Export/BOM/
- Fetches datasheets for BME280, STM32F4, power regulators, etc.
- Analyzes schematics in Export/Documentation/
- Documents I2C bus connections and addresses
- Maps power rails (3.3V, 5V)
- Generates comprehensive hardware_report.md

Result: Complete technical documentation explaining the entire system
```

### Example 2: Understanding Component Interfaces

```
User: Here are my design files. I need to know how the microcontroller interfaces with the sensors.

Agent: I'm analyzing your schematics and BOM to document all interfaces...

[Agent provides]:
### Communication Interfaces

**I2C Bus**
- Master: STM32F407VGT6
- Slaves:
  - BME280 (Temperature/Pressure sensor) at address 0x76
  - MPU6050 (Accelerometer) at address 0x68
- Pull-up resistors: 4.7kΩ on SCL and SDA
- Purpose: Sensor data acquisition

**SPI Bus**
- Master: STM32F407VGT6
- Slave: W25Q128 (Flash memory)
- CS: PA4, SCK: PA5, MISO: PA6, MOSI: PA7
- Purpose: Data logging storage
```

### Example 3: Power Analysis

```
User: Can you analyze the power distribution in my PCB?

Agent: I'll examine the power architecture from your schematics...

[Agent documents]:
### Power Distribution

**5V Rail**
- Source: USB VBUS or external DC jack
- Regulation: AMS1117-5.0 LDO
- Loads: Display module (max 200mA), STM32 pre-regulator
- Current Budget: ~500mA total

**3.3V Rail**
- Source: AMS1117-3.3 LDO (from 5V rail)
- Loads: STM32F4 (typ 50mA), sensors (total 20mA), flash memory (typ 15mA)
- Current Budget: ~100mA total
- Decoupling: 10µF bulk + 100nF ceramic per IC
```

## Component Analysis Methodology

For each component in the BOM, the agent:

1. **Identifies**: Part number, manufacturer, description
2. **Researches**: Finds official datasheet online
3. **Extracts**:
   - Primary function and purpose
   - Electrical characteristics (voltage, current, power)
   - Absolute maximum ratings
   - Communication interfaces
   - Pin functions
   - Operating conditions

## Hardware Report Structure

The generated `hardware_report.md` includes:

```markdown
# Hardware Analysis Report

## Executive Summary
[What the PCB does]

## System Architecture
[High-level functional blocks and interactions]

## Component Analysis
### [Category - e.g., Microcontroller]
#### [Part Number]
- Function
- Key Specifications
- Interfaces Used
- Role in System

## Communication Interfaces
[Complete I2C, SPI, UART, CAN bus documentation]

## Power Distribution
[Rails, regulators, current budgets]

## Detailed Functional Description
[How the board operates, signal flow, data processing]

## Critical Design Notes
[Important observations and considerations]

## Component Summary Table
[Complete component list with categories and functions]
```

## Key Features

### ✅ Comprehensive Component Research
Automatically finds and analyzes datasheets for every component in the BOM.

### ✅ Interface Documentation
Maps all digital communication buses with addresses, pin assignments, and purposes.

### ✅ Power Architecture Analysis
Documents voltage rails, regulators, current budgets, and power sequencing.

### ✅ Technical Accuracy
All specifications verified against official manufacturer datasheets.

### ✅ Signal Flow Understanding
Traces signals from inputs through processing to outputs.

### ✅ Design Quality Assessment
Notes design decisions, potential issues, and areas for optimization.

### ✅ Bilingual Support
Understands and responds in Italian and English.

## Agent Rules

The agent follows these core principles:

1. ✅ **Export Folder Only**: ONLY analyzes files in Export/BOM and Export/Documentation
2. ✅ **No Native CAD Files**: NEVER reads KiCad, Eagle, Altium, or other CAD formats
3. ✅ **Complete Component Research**: Finds datasheet for every BOM component
4. ✅ **Precise Documentation**: Uses actual signal names, designators, and specifications
5. ✅ **Cross-Referenced**: Connects datasheet info with schematic observations
6. ✅ **Quality Verification**: All claims supported by datasheets or schematics

## Best Practices

### When to Invoke the Agent

- After completing PCB design and exporting documentation
- When you need to understand an existing PCB design
- For design review and verification
- To prepare documentation for manufacturing
- When onboarding team members to a hardware project
- Before modifying an existing design

### Preparing Your Project

**Required Setup:**
```
project/
├── Export/
│   ├── BOM/
│   │   └── bill_of_materials.csv  (or .xlsx, .txt)
│   └── Documentation/
│       └── schematic.pdf
```

**Supported BOM Formats:**
- CSV files
- Excel files (.xlsx, .xls)
- Text files with component lists

**Supported Schematic Formats:**
- PDF exports
- Multi-page PDF schematics
- Annotated schematics with designators and values

### Communicating with the Agent

**Clear and Specific:**
```
✅ "Analyze my temperature monitoring PCB design and create hardware documentation"
✅ "Document all the I2C devices and their addresses in my design"
✅ "Explain how the STM32 interfaces with the sensors in this board"
```

**To Avoid:**
```
❌ "Look at my PCB" (without Export folders)
❌ "Read my KiCad files" (agent doesn't read native CAD formats)
❌ "Analyze this" (without context about what you need)
```

**Effective Requests:**
```
✅ "I've exported my BOM and schematics to the Export folders. Please analyze the design."
✅ "Create complete hardware documentation for my IoT data logger board"
✅ "Explain the power distribution architecture in my PCB"
```

## Troubleshooting

### Agent doesn't activate automatically

- Use direct invocation: `/pcb-hardware-analyst`
- Verify the file is in `.claude/agents/`

### Agent can't find files

**Check folder structure:**
```
✅ Files in Export/BOM/ folder
✅ Files in Export/Documentation/ folder
❌ Files in project root
❌ Native CAD files instead of exports
```

### Missing datasheet information

- Agent will note when datasheets cannot be found online
- Provides analysis based on component markings and categories
- Suggests manual datasheet addition if critical

### Incomplete analysis

- Ensure BOM includes all components with part numbers
- Export complete schematics showing all connections
- Include all schematic pages if multi-page design

### Report lacks specific details

- Verify schematics show signal names and net labels
- Ensure BOM has complete part numbers, not generic descriptions
- Add annotations to schematics for clarity

## When Clarification is Needed

The agent will ask for clarification if:
- Export folders are missing or empty
- Datasheets cannot be found for critical components
- Schematic connections are ambiguous
- BOM and schematic information conflicts
- Board purpose is unclear

## Quality Assurance

The agent verifies before finalizing:
- ✅ Every BOM component is researched and documented
- ✅ All communication interfaces identified and described
- ✅ Power architecture fully mapped
- ✅ Report provides complete understanding of PCB functionality
- ✅ All specifications verified against datasheets

## Customization

To modify the agent behavior:

1. Open `.claude/agents/pcb-hardware-analyst.md`
2. Modify the YAML frontmatter to change:
   - `model`: Model to use (sonnet, opus, haiku)
3. Modify the markdown content to change:
   - Analysis depth and focus areas
   - Report structure and sections
   - Component categorization approach
   - Specific interface types to prioritize

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
