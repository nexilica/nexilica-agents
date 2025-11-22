# FW/ Agents Catalog

**Quick reference for firmware development and analysis agents.**

---

## 🎯 Quick Start

### Available Agents (1)

FW/ currently contains **1 specialized agent** for STM32 firmware analysis:

**stm32-firmware-analyzer**: Comprehensive STM32 firmware analysis and documentation

**No orchestrator yet** - as more FW agents are added, consider creating `fw-workflow-orchestrator`.

---

## 📋 Task → Agent Quick Reference

| Your Task | Call This Agent | Output |
|-----------|----------------|--------|
| **Analyze STM32 firmware** | `stm32-firmware-analyzer` | Complete firmware analysis report |
| **Understand peripheral config** | `stm32-firmware-analyzer` | Peripheral initialization breakdown |
| **Memory map analysis** | `stm32-firmware-analyzer` | Memory layout and usage |
| **HAL/LL usage review** | `stm32-firmware-analyzer` | HAL library usage patterns |

---

## 📦 Available Agent

### stm32-firmware-analyzer

**Purpose**: Comprehensive STM32 firmware project analysis

**What it does**:
- Analyzes STM32CubeMX configuration
- Examines peripheral initialization (GPIO, UART, SPI, I2C, ADC, etc.)
- Reviews interrupt handlers and DMA usage
- Maps memory layout (Flash, RAM, stack, heap)
- Identifies HAL/LL library usage patterns
- Analyzes RTOS configuration (if FreeRTOS present)
- Reviews clock configuration
- Generates comprehensive firmware analysis report

**Input**:
- STM32 firmware project directory
- Source files (.c, .h)
- CubeMX configuration files (.ioc)
- Linker scripts (.ld)

**Output**:
- `firmware_analysis.md`: Complete analysis report
  - Project overview
  - MCU configuration
  - Peripheral usage breakdown
  - Memory map
  - Code structure analysis
  - Recommendations for optimization

**When to use**:
- Initial firmware project understanding
- Reverse engineering existing STM32 code
- Code review and optimization planning
- Documentation generation for handoff
- Technical debt assessment

**Typical analysis includes**:
- MCU family and specific model
- Clock tree configuration
- Peripheral initialization sequences
- Interrupt priorities and handlers
- DMA channel assignments
- Pin multiplexing and GPIO configuration
- Communication protocols setup
- RTOS tasks and synchronization (if applicable)

**File**: `stm32-firmware-analyzer.md`

---

## 🔄 Common Workflow Patterns

### Pattern 1: Firmware Understanding
```
stm32-firmware-analyzer
    ↓
Complete analysis report generated
    ↓
[User reviews findings]
    ↓
[Optional: Manual code modifications or further analysis]
```

### Future Pattern: Firmware Development Workflow
```
[When more FW agents exist]

fw-context-scanner
    ↓
stm32-firmware-analyzer
    ↓
fw-code-generator (peripheral drivers, HAL wrappers)
    ↓
fw-documenter
    ↓
fw-tester (unit tests, integration tests)
```

---

## 📁 Output Locations

Agent writes to: **`project-context/FW/{project-name}/`**

```
project-context/
└── FW/
    └── your-firmware-project/
        ├── firmware_analysis.md     ← stm32-firmware-analyzer
        ├── memory_map_report.md     ← stm32-firmware-analyzer
        ├── peripheral_config.md     ← stm32-firmware-analyzer
        └── _project_metadata.json   ← Tracking info
```

---

## 💡 Tips for Claude Code

### When to Use stm32-firmware-analyzer

**Use when**:
- User provides STM32 firmware project directory
- User asks to "analyze firmware", "understand STM32 code"
- User requests "peripheral configuration review"
- User needs "memory layout analysis"
- Reverse engineering STM32 firmware
- Firmware documentation needed

### Analysis Scope

The analyzer can handle:
- ✅ STM32 HAL-based projects
- ✅ STM32 LL (Low-Layer) projects
- ✅ Mixed HAL/LL projects
- ✅ FreeRTOS-based firmware
- ✅ Bare-metal firmware
- ✅ CubeMX-generated projects
- ✅ Hand-written firmware

### Future Expansion Suggestions

Consider adding to FW/:
1. **fw-context-scanner**: Fast firmware scanning (atomic pattern)
2. **fw-peripheral-generator**: Generate peripheral driver code
3. **fw-hal-wrapper**: Create custom HAL wrappers
4. **fw-test-generator**: Generate unit tests for firmware
5. **fw-workflow-orchestrator**: Coordinate firmware development workflow

This would enable atomic firmware development similar to SW/ category.

---

## 🎓 Examples for Claude Code

### Example 1: User Provides STM32 Project

**Your decision**:
```
User: "Analyze this STM32 firmware project"
  ↓
Read FW/agents/README.md
  ↓
Task = STM32 firmware analysis → stm32-firmware-analyzer
  ↓
Call: /stm32-firmware-analyzer with project path
  ↓
Return firmware_analysis.md location
```

### Example 2: User Asks About Specific Peripheral

**Your decision**:
```
User: "How is UART configured in this STM32 code?"
  ↓
Read FW/agents/README.md
  ↓
Task = peripheral config analysis → stm32-firmware-analyzer
  ↓
Call: /stm32-firmware-analyzer focusing on UART
  ↓
Extract UART section from analysis report
```

---

## 🔗 Related Documentation

- **Agent details**: See `stm32-firmware-analyzer.md` in this directory
- **Creating new FW agents**: See `../../meta-agent.md`
- **Atomic architecture**: See `../../README.md`

---

**Last Updated**: 2025-11-22
**Agent Count**: 1
**Category**: Firmware Development & Analysis
**Specialization**: STM32 microcontrollers
