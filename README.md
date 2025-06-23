UART Design & Verification using SystemVerilog
Project Overview
----------------
This project demonstrates the design and functional verification of a UART (Universal Asynchronous
Receiver Transmitter)
using Verilog RTL and a SystemVerilog-based testbench with UVM-style architecture (environment, driver,
generator, monitor, scoreboard).
Focus: Functional verification of TX and RX UART modules with stimulus generation, data checking, and
coverage-style validation.
Features
--------
- Configurable baud rate and clock frequency
- UART Transmitter (uarttx)
- UART Receiver (uartrx)
- Top Module integration (uart_top)
- Interface (uart_if) for seamless TB-DUT interaction
- UVM-style Testbench Components: Generator, Driver, Monitor, Scoreboard, Environment
- Support for write and read operations
- Visual simulation trace with $dumpfile("dump.vcd")
UART Architecture
-----------------
TX Input Data (dintx) --> uarttx --> tx line --> Receiver uartrx --> Received Output (doutrx)
File Structure
--------------
uart_top.sv - Top-level UART wrapper
uarttx.sv - UART transmitter module
uartrx.sv - UART receiver module
uart_if.sv - Interface for testbench-DUT
transaction.sv - Transaction class
generator.sv - Generates stimulus
driver.sv - Drives stimulus to DUT
monitor.sv - Monitors DUT response
scoreboard.sv - Compares outputs
environment.sv - Connects all TB components
tb.sv - Top-level testbench
dump.vcd - Waveform output file
README.md - Project documentation
Simulation Parameters
---------------------
clk_freq : 1,000,000 Hz
baud_rate : 9600
Data Width: 8 bits
TX Line Idle: 1 (high)
RX Sampled : Rising Edge of uclk
Testbench Operation
-------------------
- Randomized transactions for TX and RX
- Events used to synchronize driver, generator, monitor, and scoreboard
- TX -> RX data path tested
- Results are compared using a scoreboard
Example Output
--------------
[GEN]: Oper : write Din : 152
[DRV]: Data Sent : 152
[MON]: DATA SEND on UART TX 152
[SCO]: DRV : 152 MON : 152
DATA MATCHED
----------------------------------------
[GEN]: Oper : read Din : 221
[DRV]: Data RCVD : 173
[MON]: DATA RCVD RX 173
[SCO]: DRV : 221 MON : 173
DATA MISMATCHED
How to Run
----------
1. Compile & Simulate (Icarus Verilog):
 iverilog -g2012 -o uart_tb tb.sv uart_top.sv
 vvp uart_tb
 gtkwave dump.vcd
2. Vivado Simulation:
 - Create new simulation project
 - Add all .sv and uart_top.sv files
 - Set tb as the top module
 - Run behavioral simulation
Future Enhancements
-------------------
- Add parity bit support
- Extend to 9-bit/variable data width
- Add timeout and framing error detection
- Include coverage collection metrics
