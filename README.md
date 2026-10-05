Pep/9 Simulator
A browser-based simulator for the Pep/9 virtual machine, the 16-bit teaching computer used in Computer Systems by J. Stanley Warford and Computer Science Illuminated by Dale & Lewis.

▶ Open the simulator: https://ezeh-cs-teaching.github.io/pep9/
It runs entirely in your browser on Windows, macOS, Linux, Chromebooks, tablets and phones, with nothing to install and no account needed. Your work is saved in your browser between visits.
---
Features
Assembler
The full Pep/9 instruction set and all eight addressing modes (`i`, `d`, `n`, `s`, `sf`, `x`, `sx`, `sfx`)
Dot commands: `.ADDRSS`, `.ALIGN`, `.ASCII`, `.BLOCK`, `.BYTE`, `.END`, `.EQUATE`, `.WORD`
Symbols, decimal, hex, character and string constants, and escape sequences (`\n`, `\t`, `\xHH`, …)
`charIn` and `charOut` predefined
Error messages with line numbers; click an error to jump to its line
Assembler listing with a symbol table, and a Format button that realigns source into Pep/9 columns
Machine language
Type or paste object code directly (hex bytes ending with `zz`), then load, run or debug it
CPU and memory
A front panel showing A, X, SP, PC, the instruction specifier and operand specifier as bit lamps, with hex and decimal values
The decoded last instruction, its operand, and the NZVC status bits
A full 64 KB memory dump that marks the PC, the SP and the bytes just written
A run-time stack view
Debugger
Step, step over, step out, continue, and pause (useful for infinite loops)
Breakpoints: click the dot beside any instruction in the listing
Data-flow animation: each step shows values moving between memory and registers. Loads travel from memory into the CPU, stores travel from the CPU into memory, and indirect modes show the pointer fetch first. Speed is Normal, Slow or Off.
Input and output
Batch I/O: type all input before running
Terminal I/O: type input while the program runs; it pauses when it needs input
Supports `DECI`, `DECO`, `HEXO`, `STRO` and memory-mapped I/O through `charIn`/`charOut`
Other
Built-in example programs
Open and save `.pep`, `.pepo` and `.pepl` files
Light and dark themes
Responsive layout; on phones, tabs switch between Code, CPU, I/O and Memory
---
Quick start
Open the simulator.
Choose a program from Examples, or type your own in the Source tab. Every program must end with `.END`.
If the program reads input, type it in Batch I/O first (for example `25 17`).
Click Run. Output appears in the I/O panel.
Click Debug to pause before the first instruction, then click Step to execute one instruction at a time and watch the registers and memory change.
Example
```
;Read two integers and print their sum
         DECI    num1,d      ;Read the first number
         DECI    num2,d      ;Read the second number
         LDWA    num1,d      ;A <- num1
         ADDA    num2,d      ;A <- A + num2
         STWA    sum,d       ;sum <- A
         DECO    sum,d       ;Print the sum
         STOP
num1:    .BLOCK  2
num2:    .BLOCK  2
sum:     .BLOCK  2
         .END
```
Input: `25 17` → Output: `42`
Machine language example
Paste this into the Object code tab and click Run object to print `Hi`:
```
D0 00 48 F1 FC 16 D0 00 69 F1 FC 16 00 zz
```
---
Keyboard shortcuts
Keys	Action
Ctrl/Cmd + Enter	Run
Ctrl/Cmd + Shift + Enter	Debug
Ctrl/Cmd + B	Assemble
S	Step (while paused)
O	Step over
U	Step out
C	Continue
Esc	Stop
---
Memory map
Address	Contents
`0000`	Programs load here
`FB8F`	Start of the user stack (grows toward lower addresses)
`FC15`	`charIn`, memory-mapped input
`FC16`	`charOut`, memory-mapped output
`FC17`–`FFFF`	Operating system region (read-only)
`FFF4`–`FFFF`	Machine vectors
---
Differences from the desktop Pep/9 application
-----------------------------------------------
This simulator covers the parts of Pep/9 used in introductory courses. Compared with Warford's desktop application:
Trap instructions (`DECI`, `DECO`, `HEXO`, `STRO`, `NOP0`, `NOP1`, `NOP`) run as single instructions with the same effect as the operating system routines. The operating system's own code is not loaded, so you cannot step into it.
Memory trace uses a run-time stack table instead of the graphical stack-frame view driven by trace tags such as `#2d`.
Not included: Redefine Mnemonics, assembling or installing a custom operating system (`.BURN`), and the microcode-level Pep/9 CPU, which is a separate program.
If a program behaves differently here than in the desktop application, please report it (see below).
---
Reporting problems
------------------------------------------------
Open an issue describing what you expected, what happened, and the program source if possible. Students can also contact their instructor.
---
Running a copy
------------------------------------------------
The simulator is a single self-contained file, `index.html`. To run it offline, download that file and open it in any modern browser. To host your own copy, upload it to any static web host, such as GitHub Pages, Netlify or Cloudflare Pages.
---
Credits
Pep/9 was designed by J. Stanley Warford (Pepperdine University). This is an independent web implementation for teaching. It is not affiliated with or endorsed by the author or the publishers of the textbooks above.
Maintained by Dubem Ezeh.
