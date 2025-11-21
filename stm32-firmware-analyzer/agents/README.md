# STM32 Firmware Analyzer Agent - User Guide

## Files Created

- `stm32-firmware-analyzer.md` - Complete agent configuration

## How to Use the Agent

### Method 1: Direct Invocation

You can invoke the agent directly in your Claude Code conversations using:

```
/stm32-firmware-analyzer
```

This will activate the specialized agent that follows all defined rules.

### Method 2: Automatic Invocation

Claude Code can automatically invoke this agent when you:
- Mention working with STM32 microcontrollers
- Detect STM32 project files or folder structures
- Request firmware analysis or documentation
- Need explanation of embedded C code
- Ask for context about existing STM32 firmware
- Discuss STM32 peripheral configuration

### Method 3: Generation with Claude (Recommended for Customizations)

If you want to modify or regenerate the agent:

1. Run `/agents` in Claude Code
2. Select "generate with claude (recommended)"
3. Describe the modifications you want
4. Claude will generate a new version

## Main Functionality

### 1. Automatic Microcontroller Identification

The agent automatically identifies your STM32 model by examining:
- main.h header files
- Startup files (startup_stm32*.s)
- Linker scripts (.ld files)
- Configuration files (system_stm32*.c)
- Project configuration files

Once identified, it retrieves official STMicroelectronics documentation.

### 2. Official Documentation Retrieval

Uses web search to fetch:
- STM32 datasheets from st.com
- Reference manuals for peripherals
- Programming manuals for CPU architecture
- Application notes for specific features

Extracts key specifications:
- CPU architecture (Cortex-M0/M0+/M3/M4/M7)
- Clock speeds (maximum and typical)
- Memory configuration (Flash and RAM sizes)
- Available peripherals (GPIO, UART, SPI, I2C, ADC, DAC, Timers, DMA, etc.)
- Special features and capabilities

### 3. Comprehensive Firmware Analysis

Analyzes the complete codebase focusing on:

**Initialization Sequences**
- System clock configuration
- Peripheral initialization order
- GPIO configuration
- Interrupt vector setup

**Peripheral Usage**
- GPIO configuration and usage
- UART/USART communication
- SPI and I2C interfaces
- ADC/DAC setup and sampling
- Timer configuration (PWM, input capture, etc.)
- DMA channels and transfers
- Interrupt handlers and priorities

**Clock Configuration**
- Clock source (HSI/HSE/PLL)
- System clock frequency
- Peripheral clock enables
- Prescalers and dividers

**Memory Usage**
- Flash utilization
- RAM allocation
- Special memory sections (.data, .bss, heap, stack)
- Linker script analysis

**Real-Time Constraints**
- Interrupt latencies
- Timing-critical sections
- RTOS usage (if applicable)
- Task scheduling

### 4. Development Framework Detection

Identifies and analyzes:
- **STM32 HAL (Hardware Abstraction Layer)**: Modern high-level API
- **STM32 LL (Low-Layer)**: Optimized low-level API
- **CMSIS**: ARM Cortex Microcontroller Software Interface Standard
- **Bare-metal**: Direct register access
- **FreeRTOS**: Real-time operating system
- **Other RTOS**: ThreadX, embOS, etc.

### 5. Project Structure Analysis

Maps complete directory tree:
- Core system files
- Peripheral drivers
- Application code
- Configuration files
- Third-party libraries
- Middleware components

Categorizes files by function and purpose.

### 6. Firmware Report Generation

Creates `firmware_report.md` with:
- Microcontroller specifications
- Project overview and purpose
- Complete project structure
- Firmware architecture details
- Initialization sequences
- Peripheral configurations
- Memory usage analysis
- Interrupt handlers
- Program flow description
- Code quality assessment
- Dependencies and interfaces

## Firmware Report Structure

The generated `firmware_report.md` includes:

```markdown
# STM32 Firmware Analysis Report

## 1. Microcontroller Specifications
- Model, Core, Flash, RAM, Max Clock
- Key Peripherals
- Datasheet Reference

## 2. Project Overview
- Purpose and main functionality
- Development framework
- Build system
- Key features

## 3. Project Structure
[Complete directory tree with annotations]

### File Organization
- Core System Files
- Peripheral Drivers
- Application Code
- Configuration
- Third-party Libraries

## 4. Firmware Architecture

### 4.1 Initialization Sequence
[Step-by-step startup and init]

### 4.2 Clock Configuration
[System clock source, frequency, peripheral clocks]

### 4.3 Peripheral Configuration
[Detailed config for each peripheral]

### 4.4 Memory Map
[Flash and RAM usage, special sections]

### 4.5 Interrupt Handlers
[All IRQ handlers and their functions]

## 5. Program Flow
- Main loop description
- State machines (if applicable)
- Critical timing requirements

## 6. Code Quality Assessment
- Strengths
- Areas for improvement
- Best practices compliance

## 7. Dependencies and External Interfaces
- Hardware dependencies
- Software dependencies
- Communication protocols

## 8. Notes for AI Agents
[Context for code modification and improvement]
```

## Example Usage Scenarios

### Example 1: New Project Analysis

```
User: I've just finished implementing the UART driver for the STM32F407. Can you help me understand the overall structure?

Agent: I'll analyze your STM32F407 project...

[Agent performs]:
- Identifies STM32F407VGT6 from project files
- Fetches official datasheet and reference manual
- Analyzes clock configuration (168 MHz from PLL)
- Documents UART peripheral setup (baud rate, pins, interrupts)
- Maps complete initialization sequence
- Generates comprehensive firmware_report.md

Result: Complete understanding of firmware architecture and UART implementation
```

### Example 2: Low-Power IoT Device

```
User: I'm working with an STM32L476RG for a low-power IoT device. Here's my current project structure.

Agent: Let me analyze your STM32L476RG low-power project...

[Agent analyzes]:
- Microcontroller: STM32L476RG (Cortex-M4, ultra-low-power)
- Clock: MSI (Multispeed Internal) for low power
- Peripherals: LPUART, RTC, ADC in low-power mode
- Power management: Sleep modes, voltage scaling
- Framework: STM32 HAL with FreeRTOS

[Report includes]:
- Low-power strategies employed
- Wake-up sources and triggers
- Power consumption estimates
- Battery life considerations
```

### Example 3: Existing Project Analysis

```
User: Here's my STM32F103 project folder with all the source files.

Agent: I'm analyzing your STM32F103 firmware...

[Agent discovers]:
- Microcontroller: STM32F103C8T6 (Blue Pill board)
- Development: Bare-metal with direct register access
- Peripherals:
  - USART1 for serial communication
  - SPI1 for sensor interface
  - TIM2 for PWM output
  - ADC1 for analog input
- Application: Motor control with sensor feedback

[Generates detailed report explaining control loop implementation]
```

## Key Features

### ✅ Automatic Model Detection
Identifies STM32 microcontroller model without user input.

### ✅ Official Documentation Access
Retrieves and references current datasheets and reference manuals from STMicroelectronics.

### ✅ Complete Peripheral Analysis
Documents every peripheral configuration and usage pattern.

### ✅ Framework Recognition
Identifies HAL, LL, CMSIS, or bare-metal implementations.

### ✅ Real-Time Awareness
Considers timing constraints, interrupt priorities, and RTOS usage.

### ✅ Memory Optimization Insights
Analyzes Flash and RAM usage for optimization opportunities.

### ✅ AI-Optimized Documentation
Report format designed for both human and AI agent consumption.

### ✅ Code Quality Assessment
Identifies strengths and areas for improvement.

## Agent Rules

The agent follows these core principles:

1. ✅ **Verify Microcontroller Model**: Check multiple sources for accurate identification
2. ✅ **Fetch Official Documentation**: Always retrieve current datasheets from st.com
3. ✅ **Complete Analysis**: Document every aspect of firmware architecture
4. ✅ **Think Like Firmware Engineer**: Consider timing, power, hardware constraints
5. ✅ **AI-Readable Structure**: Organize information for quick access by AI agents
6. ✅ **Flag Concerns Proactively**: Note potential bugs, race conditions, resource conflicts
7. ✅ **Document Assumptions**: State assumptions when information isn't explicit
8. ✅ **Use Precise Terminology**: Employ standard embedded systems vocabulary

## Operational Guidelines

### Thoroughness But Concise
- Every section adds value
- Avoids redundancy
- Comprehensive without verbosity

### Firmware Engineering Perspective
- Considers timing constraints
- Evaluates power consumption
- Respects hardware limitations
- Identifies real-time requirements

### Documentation Quality
- Structured for easy navigation
- Cross-referenced sections
- External links to official resources
- Clear technical language

## Best Practices

### When to Invoke the Agent

- After completing STM32 firmware development
- Before modifying existing STM32 projects
- For firmware code review
- When onboarding team members
- To prepare context for code improvements
- For documentation and knowledge transfer

### Preparing Your Project

**Optimal Setup:**
```
✅ Complete STM32 project with all source files
✅ Clear microcontroller model in project files
✅ Organized folder structure (Core, Drivers, Application)
✅ Build system files (Makefile, CMakeLists.txt, or IDE project)
```

**Minimum Requirements:**
```
✅ At least main.c and initialization code
✅ Identifiable STM32 microcontroller model
✅ Basic project structure
```

### Communicating with the Agent

**Clear and Specific:**
```
✅ "Analyze my STM32F407 motor control firmware"
✅ "I need documentation for this STM32L4 low-power sensor node"
✅ "Explain the peripheral configuration in my STM32F103 project"
```

**To Avoid:**
```
❌ "Look at my embedded code" (not specific to STM32)
❌ "Analyze this" (without context)
```

**Effective Requests:**
```
✅ "I'm working with an STM32F4 for a data logger. Analyze the firmware."
✅ "Create comprehensive documentation for my STM32 USB device project"
✅ "Explain how the interrupts are configured in this firmware"
```

## Microcontroller Identification Process

The agent examines multiple sources:

1. **main.h or stm32XXxx.h headers**: Contains device-specific includes
2. **Startup files**: startup_stm32f407xx.s indicates F407 family
3. **Linker scripts**: STM32F407VGTx_FLASH.ld specifies exact model
4. **System files**: system_stm32f4xx.c indicates F4 family
5. **Project configuration**: IDE settings, CMakeLists.txt, Makefile

If ambiguous, the agent asks for clarification before proceeding.

## Quality Assurance

Before finalizing the report, the agent verifies:
- ✅ Microcontroller specifications match official datasheet
- ✅ Project structure diagram is complete and accurate
- ✅ All peripheral configurations are documented
- ✅ Report is well-formatted and easy to navigate
- ✅ Another AI agent could use this to modify code intelligently
- ✅ All assumptions are clearly stated
- ✅ External links are current and correct

## Troubleshooting

### Agent doesn't activate automatically

- Use direct invocation: `/stm32-firmware-analyzer`
- Verify the file is in `.claude/agents/`

### Microcontroller model not identified

**Check these files:**
```
✅ main.h contains STM32 device header
✅ Startup file has clear model designation
✅ Linker script specifies device
```

If unclear, the agent will ask you to specify the model.

### Incomplete peripheral analysis

**Ensure:**
```
✅ Peripheral initialization code is present
✅ Configuration registers are accessible
✅ HAL/LL initialization functions are included
```

### Missing datasheet information

- The agent will note when datasheets cannot be fetched
- Provides analysis based on available information
- Suggests manual datasheet addition for complete analysis

### Report lacks specific details

**Improve by:**
```
✅ Adding comments to initialization code
✅ Including configuration header files
✅ Documenting peripheral usage in application code
```

## Integration with Other Agents

This agent works well with:
- **pcb-hardware-analyst**: Firmware + hardware documentation
- **electronics-datasheet-writer**: Complete system documentation
- Code improvement agents: Report provides necessary firmware context

**Workflow:**
```
1. pcb-hardware-analyst creates hardware_report.md
2. stm32-firmware-analyzer creates firmware_report.md
3. electronics-datasheet-writer combines both for complete datasheet
```

## Advanced Features

### RTOS Detection
Identifies and analyzes:
- FreeRTOS task configuration
- Task priorities and scheduling
- Semaphores, mutexes, queues
- Task communication patterns

### DMA Analysis
Documents:
- DMA channel assignments
- Memory-to-peripheral transfers
- DMA interrupts and callbacks
- Circular vs. normal mode

### Low-Power Modes
Analyzes:
- Sleep, Stop, and Standby modes
- Wake-up sources
- Clock gating strategies
- Power consumption optimization

## Customization

To modify the agent behavior:

1. Open `.claude/agents/stm32-firmware-analyzer.md`
2. Modify the YAML frontmatter to change:
   - `model`: Model to use (sonnet, opus, haiku)
   - `color`: Agent color in the UI
3. Modify the markdown content to change:
   - Analysis depth and focus
   - Report structure and sections
   - Peripheral types to emphasize
   - Code quality criteria

## Support

For issues or questions:
- Consult official documentation: https://code.claude.com/docs/en/sub-agents.md
- Use `/help` in Claude Code
- Ask Claude Code directly about the agent's behavior

## Resources

- **STMicroelectronics**: https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html
- **STM32 Documentation**: Datasheets, reference manuals, programming guides
- **ARM Cortex-M**: ARM Architecture Reference Manual

---

**Agent Version**: 1.0
**Model**: Sonnet
**Color**: Cyan
**Specialization**: STM32 Microcontrollers, Embedded C, Firmware Architecture
**Created**: 2025-11-21
