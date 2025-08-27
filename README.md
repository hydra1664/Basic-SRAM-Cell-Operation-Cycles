# Basic SRAM Cell Simulation

This project is about building and simulating a simple 1-bit SRAM (Static Random Access Memory) cell in Logisim Evolution. The design is based on an SR latch constructed from NAND gates, with word-line and bit-line control for read and write operations. I wanted to understand how memory cells work at the circuit level and see how read and write cycles can be implemented with just a few basic gates.

All the circuit files are uploaded in the folder named **Circuit Files**, and I have also included a PDF in this repository that contains images of the main circuit along with snapshots of the input and output behavior during testing.

## Objective
The main goals of this project were:
- To design a single-bit SRAM cell using only NAND gates
- To learn how data is written to and read from the memory cell
- To observe the SR latch behavior under different input conditions
- To gain a practical understanding of memory storage at the logic level

## Components Used
- 4 NAND gates
  - 2 for the SR latch
  - 2 for access control
- 3 input pins
  - WL (Word Line)
  - BL (Bit Line)
  - BL_bar (Complement of Bit Line)
- 2 LEDs
  - Q and Q_bar (to show stored value)

## Design
The latch is created by cross-connecting two NAND gates. The word line (WL) acts as the access signal. When WL is active, the bit line and its complement control whether the latch stores a 0 or a 1. When WL is inactive, the latch holds its state and the outputs remain stable.

## Write Operation
- Enable WL
- Set BL and BL_bar to complementary values
- BL = 0 and BL_bar = 1 writes a 1 into the cell (Q = 1)
- BL = 1 and BL_bar = 0 writes a 0 into the cell (Q = 0)

## Read Operation
- Disable WL (set it to 0)
- The latch holds the previously stored value
- Q and Q_bar LEDs display the stored state

## Truth Table

| WL | BL | BL_bar | Operation        | Q (after) | Q_bar (after) |
|----|----|--------|-----------------|-----------|---------------|
| 0  | X  | X      | Hold / Read     | Previous  | Previous      |
| 1  | 0  | 1      | Write 1         | 1         | 0             |
| 1  | 1  | 0      | Write 0         | 0         | 1             |
| 1  | 0  | 0      | Hold (no effect)| Previous  | Previous      |
| 1  | 1  | 1      | Invalid state   | 1         | 1             |

## Troubleshooting Notes
At first, I mistakenly applied BL = 1 and BL_bar = 0 to try writing a 1, which resulted in the opposite output. After checking the latch logic, I realized that the SR latch with NAND gates works with active-low inputs. Fixing the input combinations solved the issue:
- To write 1, use BL = 0, BL_bar = 1
- To write 0, use BL = 1, BL_bar = 0

Common issues I ran into:
- Forgetting to enable WL during a write (output wouldn’t update)
- Accidentally setting both BL and BL_bar to 1 (invalid state, both LEDs on)
- Leaving BL and BL_bar both at 0, which just holds the last state

## Conclusion
This project gave me a clear, hands-on understanding of how a basic SRAM cell works. By building it from simple gates in Logisim Evolution, I was able to see exactly how read and write cycles are controlled and how the latch preserves data. It was also a good exercise in debugging and understanding active-low logic.  
