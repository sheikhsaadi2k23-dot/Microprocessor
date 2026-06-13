# Microprocessor and Microcontroller Laboratory
Name: Md Sheikh Saadi
ID:0432320005101005
This repository contains a collection of 8086 Assembly Language programs developed for the Microprocessor and Microcontroller Lab. The codebase covers fundamental concepts including standard Input/Output (I/O) operations, 8-bit arithmetic execution, iterative loops, conditional branching, stack isolation, and bitwise logical/rotational operations using the emu8086 emulator framework.

## System Architecture & Environment
* **Processor Architecture:** Intel 8086 (16-bit Segmented Memory Architecture)
* **Memory Model:** `SMALL` (Allocates a single data segment and a single code segment)
* **Stack Allocation:** `100H` bytes (256 bytes reserved for stack operations)
* **Interrupt Vector:** DOS Service Vector `INT 21H`

## Laboratory Catalog & Technical Analysis

### File Name: mycode(1).asm
#### Content:
* **Functional Description:** This program reads a single character from the standard keyboard input buffer and echoes it directly back to the terminal monitor screen.
* **Technical Analysis:** The module triggers two distinct configurations of the DOS service vector `INT 21H`. Loading function code `AH = 01H` suspends execution until a key is registered, storing its hexadecimal ASCII footprint in `AL`. The byte is subsequently mapped into the data register `DL`, and function code `AH = 02H` is called to dispatch the character straight to the console buffer output pipeline.

### File Name: mycode2.asm
#### Content:
* **Functional Description:** This script defines two static 8-bit values (2 and 3), evaluates their mathematical summation, and projects the resulting integer text onto the display window.
* **Technical Analysis:** Immediate numeric constraints are mapped into registers `AL` and `BL`. Executing `ADD AL, BL` updates the accumulator destination register `AL` with the binary sum `05H`. Because native binary vectors are not human-readable on terminal environments, `ADD AL, 30H` scales the integer to its equivalent ASCII code point character '5' (Hex `35H`) before calling the `INT 21H` interrupt.

### File Name: mycode3.asm
#### Content:
* **Functional Description:** This program executes an 8-bit subtraction sequence on pre-allocated registry values, formatting the output into a valid displayable ASCII string.
* **Technical Analysis:** Following an architecture identical to the addition profile, this routine utilizes the `SUB AL, BL` processor directive. Register `AL` is loaded with 5 and `BL` with 2. Post-subtraction, the binary difference `03H` inside `AL` undergoes a `30H` bit-mask scaling to reach the ASCII representation of '3' (Hex `33H`), which is written to the display device via standard DOS subroutines.

### File Name: mycode4.asm
#### Content:
* **Functional Description:** This script demonstrates the implementation of 8-bit unsigned integer multiplication using implicit register dependencies.
* **Technical Analysis:** The assembly instruction `MUL` dictates implicit data alignment. By supplying an 8-bit target operand (`MUL BL`, where `BL = 2`), the arithmetic logic unit automatically multiplies the parameter by the contents of the primary accumulator `AL` (3). The complete product (`06H`) settles in `AX`, which is then normalized to ASCII `36H` ('6') and printed to the terminal.

### File Name: mycode5.asm
#### Content:
* **Functional Description:** This script analyzes the spatial register allocation of a division operation, calculating the quotient of 15 / 5.
* **Technical Analysis:** For an 8-bit divisor command like `DIV BL` (where `BL = 5`), the complete dividend must be structured across the 16-bit register `AX`. Accordingly, `AL` receives 15 and `AH` is padded to 0. Upon division execution, the processor isolates the resulting quotient inside `AL` (3) and pushes the remainder inside `AH` (0). The register `AL` is then scaled by `30H` to display the text character '3'.

### File Name: mycode6.asm
#### Content:
* **Functional Description:** This script loops exactly 5 times to collect user inputs, accumulates their total sum, and extracts separate multi-digit characters mathematically to handle results greater than 9.
* **Technical Analysis:** Loop parameters are defined by populating the count control register `CX = 5`. Within `input_loop`, input characters are captured, stripped of their character offset mask via `SUB AL, 30H`, and progressively added into `BL`. To prevent console display overflow for multi-digit totals, the sum is passed to `AX` and divided by `BH = 10`. The quotient in `AL` (representing the tens position) and the remainder in `AH` (representing the units position) are unpacked, shifted to ASCII format, and printed sequentially.

### File Name: mycode7.asm
#### Content:
* **Functional Description:** This module parses two individual numeric console inputs and uses conditional execution paths to identify and print the higher value.
* **Technical Analysis:** Two numeric characters are captured and processed into data registers `BL` and `BH` after removing their character masks. The `CMP AL, BH` evaluation updates internal processor arithmetic flags. The signed jump directive `JGE print_larger` (Jump if Greater than or Equal) overrides register reassignment if the primary value matches or outranks the comparison target, sending the true maximum forward to the console output stream.

### File Name: mycode8.asm
#### Content:
* **Functional Description:** This program reads a continuous sequence of three characters and evaluates their comparative order to isolate the element with the lowest ASCII value.
* **Technical Analysis:** The module stores three sequential keyboard characters inside `BL`, `BH`, and `CL`. It initiates an ordered evaluation sequence using the `CMP` operator and the signed conditional shortcut `JLE` (Jump if Less than or Equal). If the evaluated tracking byte is smaller than or equal to the comparison parameter, execution branches to prevent register modification. This isolates the absolute lowest byte and passes it to the standard display output.

### File Name: mycode9.asm
#### Content:
* **Functional Description:** Working as the exact inverse of `mycode8.asm`, this module processes three console inputs and outputs the element with the highest ASCII value.
* **Technical Analysis:** Sharing the exact structural registration setup as the minimum selection script, this program reverses the filtering criteria to locate upper boundary data points. By utilizing the `JGE` (Jump if Greater than or Equal) directive, execution branches around register updates if the tracked element outranks the comparison register. The maximum ASCII component is safely isolated inside `BL` and printed after executing a newline formatting sequence.

### File Name: mycode10.asm
#### Content:
* **Functional Description:** This program implements a nested loop architecture to construct a perfect 3x3 graphic layout of asterisk symbols (*) on the screen.
* **Technical Analysis:** Nesting iterative structures within assembly requires protecting loop metrics from being overwritten. The routine initializes `CX = 3` to control the `outer_loop` boundary and safely backs up its state onto the system stack segment using `PUSH CX`. `CX` is then safely re-allocated with 3 to handle the `inner_loop` logic, which prints asterisks (`DL = '*'`). Once an row cycle completes, a carriage return sequence is performed, and `POP CX` restores the outer tracking loop count to execute the final loop decrement check via `LOOP outer_loop`.

### File Name: mycode11.asm
#### Content:
* **Functional Description:** This script reads a digit from standard input, executes a logical right-shift operation (SHR) by one bit position, and prints the resulting character value.
* **Technical Analysis:** The module captures a character byte and normalizes it to a true integer value via `SUB AL, '0'`. The instruction `SHR AL, 1` executes a logical right shift. This shifts every bit position to the right by 1, pushes the lowest bit (LSB) into the Carry Flag (CF), and fills the vacant highest bit position (MSB) with a 0. This operation acts as an efficient hardware-level integer division by 2. The result is reformatted into displayable ASCII using `ADD DL, '0'` and printed.

### File Name: mycode12.asm
#### Content:
* **Functional Description:** This program reads a single character digit, applies a logical left-shift operation (SHL) by one bit, and displays the adjusted calculation on the screen.
* **Technical Analysis:** Following input normalization via `SUB AL, '0'`, the application executes `SHL AL, 1`. This operation shifts all bits to the left by one position; the highest bit (MSB) is pushed into the Carry Flag, and a 0 is introduced into the vacant lowest bit position (LSB). This bitwise adjustment effectively multiplies the numeric value of `AL` by 2. The script then applies formatting controls and shifts the value back to the ASCII domain using `ADD DL, '0'` before rendering it.

### File Name: mycode13.asm
#### Content:
* **Functional Description:** This program processes a numeric digit input and executes a bitwise left circular rotation (ROL) by one bit position.
* **Technical Analysis:** Unlike logical shifting operations where bits are pushed out and lost, the `ROL AL, 1` command circularizes the bitstream within the register. The bit exiting the highest position (MSB) is copied into the Carry Flag and wrapped around to fill the newly vacated lowest position (LSB). This ensures no bit data is lost. The rotated bit configuration in `BL` is then converted back to printable ASCII format and printed.

### File Name: mycode14.asm
#### Content:
* **Functional Description:** This script reads a digit from the user, executes a circular bitwise right rotation (ROR) by one position, and outputs the resulting data character.
* **Technical Analysis:** Operating as the exact structural inverse of `mycode13.asm`, this program applies the `ROR AL, 1` instruction. The bit residing at the lowest position (LSB) exits the register structure, is mirrored into the Carry Flag, and is pushed directly into the highest bit position (MSB) of the same register. Once this circular bit alignment completes, the data is adjusted back into printable ASCII using `ADD DL, '0'` and sent to the active console output pipeline.#   M i c r o p r o c e s s o r - L a b  
 