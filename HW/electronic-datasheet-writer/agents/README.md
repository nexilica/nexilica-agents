# Electronics Datasheet Writer Agent - User Guide

## Files Created

- `electronics-datasheet-writer.md` - Complete agent configuration

## How to Use the Agent

### Method 1: Direct Invocation

You can invoke the agent directly in your Claude Code conversations using:

```
/electronics-datasheet-writer
```

This will activate the specialized agent that follows all defined rules.

### Method 2: Automatic Invocation

Claude Code can automatically invoke this agent when you:
- Mention creating datasheets for electronic systems
- Have hardware/firmware report files in your project
- Request technical documentation for PCBs or sensors
- Need professional documentation for electronic designs
- Ask about generating product specifications

### Method 3: Generation with Claude (Recommended for Customizations)

If you want to modify or regenerate the agent:

1. Run `/agents` in Claude Code
2. Select "generate with claude (recommended)"
3. Describe the modifications you want
4. Claude will generate a new version

## Main Functionality

### 1. Comprehensive Technical Documentation

The agent creates professional, industry-standard datasheets for electronic systems including:
- PCBs and development boards
- Sensor modules
- Communication systems
- Data acquisition boards
- IoT devices
- Embedded systems

### 2. Multi-Source Analysis

Analyzes and synthesizes information from:
- `HW/hardware_report.md` - Hardware design documentation
- `FW/firmware_report.md` - Firmware functionality
- `SW/software_report.md` - Software interfaces

The agent adapts based on which files are available in your project.

### 3. Technical Depth and Accuracy

Provides expert-level technical detail including:
- Precise electrical and mechanical specifications
- Detailed operational theory and circuit behavior
- Reference designs and application examples
- Links to application notes, standards (IEEE, IEC, ISO)
- Circuit analysis and signal flow descriptions
- Practical implementation considerations

### 4. Structured Professional Output

Generates datasheets following industry standards with:
- Features and Applications sections
- Technical Characteristics table with MIN/TYP/MAX values
- Connector pinout documentation
- Comprehensive Application Information section
- External references to standards and documentation

## Datasheet Structure

The agent generates datasheets with the following mandatory sections:

### 1. Features
- 5-6 key system features
- Specific and measurable capabilities
- Focus on differentiators

### 2. Applications
- 5-6 typical use cases
- Real-world application scenarios
- Specific to system capabilities

### 3. Description
- Maximum 150 words
- Concise system overview
- Purpose and key benefits

### 4. Technical Characteristics
- Markdown table format
- Parameters: MIN/TYP/MAX columns
- Complete electrical, mechanical, environmental specs
- Includes power, performance, and interface specifications

### 5. Connectors Pinout
- Connector type description
- Pin number, signal name, detailed descriptions
- Electrical characteristics for each pin

### 6. Application Information
- Most comprehensive section
- Operating principles and theory
- Functional block descriptions
- Communication protocols and data formats
- Configuration and setup procedures
- Calibration and optimization techniques
- Troubleshooting guidelines
- External references to standards and app notes

## Example Usage Scenarios

### Example 1: Temperature Sensor Board

```
User: I've finished developing the temperature sensor board. Can you help me create the datasheet?

Agent: I'll analyze your project files to generate a comprehensive technical datasheet...

[Agent reads hardware_report.md and firmware_report.md]
[Generates professional datasheet with all sections]
[Includes BME280 specifications, I2C interface details, power requirements, etc.]
```

### Example 2: IoT Data Logger System

```
User: I need professional documentation for my IoT data logger system

Agent: Let me create a detailed datasheet from your hardware and firmware reports...

[Agent analyzes all available reports]
[Creates datasheet covering data acquisition, wireless communication, storage]
[Includes application examples for industrial monitoring]
```

### Example 3: Italian Language Request

```
User: Ho bisogno di un datasheet per il mio sistema di acquisizione dati

Agent: Creerò un datasheet completo in italiano analizzando i report del tuo progetto...

[Agent generates complete datasheet in Italian]
[Maintains technical accuracy with Italian terminology]
```

## Key Features

### ✅ Professional Quality
Produces industry-standard datasheets comparable to commercial documentation from major electronics manufacturers.

### ✅ Technical Accuracy
All specifications are verified against source documents. Never fabricates data or makes unsupported claims.

### ✅ Comprehensive Coverage
Analyzes hardware, firmware, and software aspects to provide complete system documentation.

### ✅ Structured Format
Follows consistent, professional formatting with clear sections and markdown tables.

### ✅ External References
Includes links to relevant application notes, standards documents, and technical resources.

### ✅ Language Flexibility
Generates datasheets in the language of your request (Italian, English, etc.).

## Agent Rules

The agent follows these core principles:

1. ✅ **Source-Based Analysis**: Only analyzes files in designated report directories (HW/, FW/, SW/)
2. ✅ **Mandatory Structure**: Always includes all required sections (Features, Applications, Description, etc.)
3. ✅ **Technical Precision**: Uses exact values with units, never vague descriptions
4. ✅ **No Fabrication**: Only states specifications verified from source documents
5. ✅ **Professional Tone**: Maintains formal, objective style of commercial datasheets
6. ✅ **Comprehensive Details**: Prioritizes completeness over brevity
7. ✅ **Quality Assurance**: Verifies numerical values, units, and table formatting before finalizing

## Writing Standards

### Technical Language
- Uses precise engineering terminology
- Includes specific values, tolerances, and ranges
- Provides context and rationale for design choices

### Quantifiable Details
- "16-bit ADC resolution with ±0.5 LSB INL" ✅
- "High resolution ADC" ❌

### Specifications Format
- Parameters with MIN/TYP/MAX values in tables
- Units clearly specified
- Environmental and operating ranges included

### External References
- Links to component datasheets
- References to industry standards (IEEE, IEC, ISO)
- Application notes and design guides

## Best Practices

### When to Invoke the Agent

- After completing electronic system design
- When preparing for manufacturing
- For product documentation and marketing materials
- When sharing designs with partners or customers
- For regulatory compliance documentation

### Preparing Your Project

**Optimal Setup:**
```
✅ Have hardware_report.md documenting PCB design
✅ Have firmware_report.md documenting embedded software
✅ Have software_report.md documenting high-level interfaces
✅ Ensure reports contain complete specifications
```

**Minimum Requirements:**
```
✅ At least one report file (HW, FW, or SW)
✅ Clear description of system purpose
✅ Basic specifications available
```

### Communicating with the Agent

**Clear and Specific:**
```
✅ "Create a datasheet for my STM32-based temperature monitoring system"
✅ "Generate technical documentation for the pressure sensor PCB"
✅ "I need a datasheet in Italian for the data acquisition board"
```

**To Avoid:**
```
❌ "Make some documentation" (too vague)
❌ "Create a datasheet" (without context about the system)
```

## Handling Missing Information

If critical specifications are missing from source documents:
- The agent notes incomplete information in the datasheet
- Uses "TBD" for specifications that cannot be determined
- Suggests what additional information would improve the datasheet
- Never fabricates or guesses specifications

## Troubleshooting

### Agent doesn't activate automatically

- Use direct invocation: `/electronics-datasheet-writer`
- Verify the file is in `.claude/agents/`

### Datasheet lacks detail

- Ensure your hardware/firmware reports contain complete specifications
- Include electrical characteristics, pin assignments, and functional descriptions
- Provide component part numbers and interface details

### Wrong language in output

- Clearly specify language in your request
- Example: "Create a datasheet in Italian"
- Example: "Generate documentation in English"

### Missing technical specifications

- The agent can only extract specifications from provided reports
- Review your source reports to ensure they contain necessary data
- Add missing specifications to reports before regenerating datasheet

## Customization

To modify the agent behavior:

1. Open `.claude/agents/electronics-datasheet-writer.md`
2. Modify the YAML frontmatter to change:
   - `model`: Model to use (sonnet, opus, haiku)
3. Modify the markdown content to change:
   - Section requirements and structure
   - Level of technical detail
   - Output formatting preferences
   - Additional sections or specialized content

## Quality Assurance Checklist

Before finalizing, the agent verifies:
- ✅ All numerical values and units are consistent
- ✅ All mandatory sections are present
- ✅ Tables are properly formatted in Markdown
- ✅ Technical accuracy against source documents
- ✅ Language consistency with user's request
- ✅ External links are relevant and properly formatted

## Support

For issues or questions:
- Consult official documentation: https://code.claude.com/docs/en/sub-agents.md
- Use `/help` in Claude Code
- Ask Claude Code directly about the agent's behavior

---

**Agent Version**: 1.0
**Model**: Sonnet
**Languages Supported**: Italian, English, and others
**Created**: 2025-11-21
