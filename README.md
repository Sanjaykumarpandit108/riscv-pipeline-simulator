# RISC-V Assembler with Pipeline Simulator

A comprehensive RISC-V assembly language assembler and 5-stage pipeline simulator written in C++. This project demonstrates the complete pipeline execution of RISC-V instructions with data forwarding, hazard detection, and control unit implementation.

## 🚀 Features

### Core Functionality
- **RISC-V Assembly to Machine Code Translation**: Converts RISC-V assembly instructions to 32-bit binary machine code
- **5-Stage Pipeline Simulation**: Implements IF (Instruction Fetch), ID (Instruction Decode), EX (Execute), MEM (Memory), WB (Write Back) stages
- **Data Forwarding**: Handles data hazards through forwarding from EX and MEM stages
- **Hazard Detection**: Detects and handles control hazards for branches and jumps
- **Control Unit**: Implements control signals for different instruction types

### Supported Instruction Types
- **R-type**: `add`, `sub`, `sll`, `slt`, `sltu`, `xor`, `srl`, `sra`, `or`, `and`
- **I-type**: `addi`, `slti`, `sltiu`, `xori`, `ori`, `andi`, `slli`, `srli`, `srai`, `jalr`, `lb`, `lh`, `lw`, `lbu`, `lhu`
- **B-type**: `beq`, `bne`, `blt`, `bge`, `bltu`, `bgeu`
- **J-type**: `jal`
- **S-type**: `sb`, `sh`, `sw`
- **U-type**: `lui`, `auipc`

### Pipeline Features
- **Register File**: 32 general-purpose registers (x0-x31)
- **Memory System**: 1024-word data memory
- **ALU Operations**: Arithmetic, logical, comparison, and shift operations
- **Branch Prediction**: Simple branch handling with pipeline flushing
- **Cycle-by-Cycle Execution**: Detailed simulation of each pipeline stage

## 📋 Prerequisites

- C++ compiler (GCC, Clang, or MSVC)
- Standard C++ libraries
- No external dependencies required

## 🛠️ Installation & Compilation

1. **Clone or download the project**
   ```bash
   git clone <your-repository-url>
   cd assembler
   ```

2. **Compile the source code**
   ```bash
   g++ -o assembler_with_pipeline assembler_with_pipeline.cpp
   ```

3. **Run the simulator**
   ```bash
   ./assembler_with_pipeline
   ```

## 🎯 Usage

### Interactive Mode
1. Run the executable
2. Choose option 1 for manual input
3. Enter RISC-V assembly instructions one by one
4. Type 'end' to finish input and start simulation

### Default Test Mode
1. Run the executable
2. Choose option 2 to use built-in test instructions
3. Watch the pipeline simulation execute

### Example Assembly Code
```assembly
addi x7, x0, 8      # Load immediate value 8 into x7
beq x7, x0, 5       # Branch if x7 equals x0
addi x3, x0, 0      # Load immediate value 0 into x3
add x1, x2, x3      # Add x2 and x3, store in x1
sub x7, x7, x12     # Subtract x12 from x7
bge x7, x11, -4     # Branch if x7 >= x11
```

## 🔧 Technical Details

### Pipeline Stages

#### 1. Instruction Fetch (IF)
- Fetches instructions from instruction memory
- Updates Program Counter (PC)
- Handles pipeline stalls and flushes

#### 2. Instruction Decode (ID)
- Decodes instruction fields (opcode, funct3, funct7, registers, immediate)
- Reads register values
- Implements data forwarding logic
- Generates control signals

#### 3. Execute (EX)
- Performs ALU operations
- Handles branch and jump instructions
- Calculates memory addresses
- Manages control hazards

#### 4. Memory (MEM)
- Performs memory read/write operations
- Handles load/store instructions
- Passes ALU results to next stage

#### 5. Write Back (WB)
- Writes results back to register file
- Handles load-to-use forwarding

### Data Forwarding
The simulator implements data forwarding to resolve data hazards:
- **EX to EX forwarding**: Forwards ALU results from current EX stage to previous EX stage
- **MEM to EX forwarding**: Forwards memory data or ALU results from MEM stage to EX stage

### Control Hazards
- **Branch Instructions**: Flushes pipeline when branch is taken
- **Jump Instructions**: Flushes pipeline and updates PC
- **Pipeline Stalls**: Prevents instruction fetch during hazards

### ALU Operations
Supported ALU operations:
- `0000`: AND
- `0001`: OR
- `0010`: ADD
- `0011`: SLL (Shift Left Logical)
- `0100`: SRL (Shift Right Logical)
- `0101`: SRA (Shift Right Arithmetic)
- `0110`: SUB
- `0111`: SLT (Set Less Than)
- `1000`: SLTU (Set Less Than Unsigned)
- `11111`: XOR

## 📊 Output Format

The simulator provides detailed output for each cycle:
- Current cycle number
- Stage-by-stage execution details
- Register values and memory operations
- Data forwarding information
- Pipeline flush and stall notifications
- Final register state

### Sample Output
```
<======================= Cycle 1 =======================>

=== INSTRUCTION FETCH STAGE ===
Current PC: 0
Fetched instruction from address 0: 00000000010000000000001110010011

=== INSTRUCTION DECODE STAGE ===
Decoding instruction: 00000000010000000000001110010011
...
```

## 🧪 Testing

The simulator includes built-in test cases that demonstrate:
- Basic arithmetic operations
- Branch instructions
- Data forwarding scenarios
- Pipeline hazards

## 🔍 Key Components

### Classes and Structures
- `controlWord`: Control signals for pipeline stages
- `IFID`: Instruction Fetch/Decode pipeline register
- `IDEX`: Instruction Decode/Execute pipeline register
- `EXMO`: Execute/Memory pipeline register
- `MOWB`: Memory/Write Back pipeline register
- `PipelineControl`: Pipeline control and hazard management
- `RiscVAssembler`: Assembly to machine code translation

### Global Variables
- `instructionMemory`: Vector storing machine code instructions
- `dataMemory`: Array simulating data memory
- `GPR`: General Purpose Registers array
- `PC`: Program Counter
- `usedRegisters`: Set tracking used registers

## 🎓 Educational Value

This project serves as an excellent learning tool for:
- Computer Architecture concepts
- Pipeline design and optimization
- RISC-V instruction set architecture
- Assembly language programming
- Hazard detection and resolution
- Control unit design

## 🤝 Contributing

Feel free to contribute to this project by:
- Adding new RISC-V instructions
- Improving pipeline efficiency
- Enhancing the user interface
- Adding more comprehensive test cases
- Optimizing the code structure

## 📝 License

This project is open source and available under the MIT License.

## 👨‍💻 Author

Created as an educational project for understanding RISC-V architecture and pipeline design.

---

**Note**: This simulator is designed for educational purposes and may not handle all edge cases or complex RISC-V features. It focuses on demonstrating core pipeline concepts and basic RISC-V instruction execution. 
