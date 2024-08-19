Pipelined RISC-V CPU | Hardware project

In this project, we designed and implemented a 5-stage pipelined CPU architecture using scala/chisel and the SBT to check our work:

Instruction Fetch (IF) Stage:
Objective: Efficiently retrieve instructions from memory.
Implementation: The IF stage fetches the next instruction from the instruction memory using the Program Counter (PC). The PC is incremented to point to the subsequent instruction, ensuring continuous instruction flow. The fetched instruction is temporarily stored in the instruction register to be passed to the next stage. A multiplexer is used to select the appropriate PC value based on branch predictions and jumps.

Instruction Decode (ID) Stage:
Objective: Decode the fetched instruction to understand its type and required operands.
Implementation: The ID stage parses the instruction to extract the opcode, source operand addresses, and destination operand address. A dedicated decoder circuit interprets the instruction format and generates control signals. The stage also involves reading the source operands from the register file. Control signals are prepared for the ALU, memory access, and write-back stages. This stage includes hazard detection logic to identify and mitigate data hazards.

Execution (EX) Stage:
Objective: Perform the arithmetic, logic, or branch operation specified by the instruction.
Implementation: The EX stage employs an Arithmetic Logic Unit (ALU) to execute operations such as addition, subtraction, logical AND, OR, and comparison. The ALU takes the operands provided by the ID stage and performs the required computation. For branch instructions, it calculates the target address. The stage uses forwarding techniques to resolve data hazards by providing operands directly from later pipeline stages when necessary, reducing stalls and improving throughput.

Memory Access (MEM) Stage:
Objective: Access data memory for load and store operations.
Implementation: The MEM stage handles instructions that require reading from or writing to data memory. For load instructions, it reads data from the memory address computed in the EX stage. For store instructions, it writes data to the specified memory address. This stage integrates a data memory interface to ensure efficient and accurate data transfer. Additionally, it includes memory hazard detection and handling mechanisms to manage potential conflicts.

Write Back (WB) Stage:
Objective: Write the result of the computation or memory access back to the register file.
Implementation: The WB stage takes the result produced by either the EX stage or the MEM stage and writes it to the destination register specified by the instruction. This update completes the instruction execution cycle. The register file supports simultaneous read and write operations to facilitate this process. The stage ensures data consistency and correctness through careful synchronization and control signal management.

Advanced Features and Optimizations:

Pipeline Hazards and Data Forwarding: Implemented hazard detection units to identify data dependencies and control hazards. Utilized data forwarding techniques to resolve hazards by bypassing data directly from pipeline registers to the ALU inputs, minimizing stalls and maintaining pipeline efficiency.

Branch Prediction: Integrated a branch prediction mechanism to guess the outcome of branch instructions, reducing the number of pipeline flushes due to incorrect branch predictions. This involves a simple prediction scheme that tracks branch history and outcomes.

Control Unit Design: Developed a sophisticated control unit to generate the necessary control signals for each pipeline stage based on the decoded instruction. The control unit ensures synchronized and coordinated operation across all stages, handling various instruction types and scenarios.

ALU Capabilities: Enhanced the ALU to support a wide range of arithmetic and logical operations required by the instruction set architecture (ISA). The ALU is designed for high-speed operation, with optimized logic circuits to reduce latency.

Register File Management: Used a multi-port register file allowing multiple read and write operations per clock cycle. This feature is crucial for supporting the high throughput of the pipelined architecture.

Memory Interface: Developed an efficient memory interface for data access operations, with mechanisms to handle load/store operations, memory alignment issues, and caching strategies to improve access speed.

Program Counter (PC) Management: Implemented a PC management system that includes support for sequential instruction fetching, jumps, and branches. The PC logic ensures correct instruction flow and handles branch targets and jump addresses effectively.
