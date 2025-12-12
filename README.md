# HP67-extended-firmware
Extends the functionality of the HP67 vintage calculator


## Description

This repository contains extended firmware for the vintage calculator HP67
from the late 1970's.
 
Unfortunately, this old calculator can not be re-flashed, so the firmware must be 
executed on HP67 simulators/emulators, for example the **x11-calc** simulator, by mike632t, 
which can be found found [here](https://github.com/mike632t/x11-calc)

The x11-calc-67 simulator can use the firmware directly, using the ROM switch (-r).


## Features

- Extends the number of storage registers to 101
- Extends the number of program steps to 448 or 896
- Adds new functionality so that the X-register can be used as a second indirect register
- Adds support to read and write up to 4 card sides (2 cards) to be able to read/write large programs


### Indirect use of the X-register 

The number in the X-register can be used to address storage registers or program labels much like the function of the I-register. The **EEX** key doubles as the (x) key if preceded by **RCL**, **STO** or **GTO**. 

#### RCL (x)

When **RCL** **EEX** is executed, the value in the storage register addressed by the number in the X-register is returned (in the X-register).

This makes it easy to recall one of the new registers. For example to recall register 99, just press **9** **9** **RCL** **EEX**

#### STO (x)

When **STO** **EEX** is executed, the value in the Y-register is stored in the register addressed by the number in the X-register. The stack is also dropped one step.

This makes it easy to store a value in of the new registers. For example to store 5 in register 99, just press **5** **ENTER** **9** **9** **STO** **EEX**

#### GTO (x)

When **GTO** **EEX** is executed, and the value in the X-register is positive 0-19, execution transfers to the next label specified by the number in the X-register. For example, 0=LBL 0, 9=LBL 9, 10=LBL A, 19=LBL e.

When **GTO** **EEX** is executed, and the value in the X-register is a negative number between -1 and -999, execution transfers back in program memory the number of steps specified by the negative number in the X-register.

#### Limitations

- GSB (x) is not supported.
- Storage register arithmetic, eg. STO + (x), is not supported.

### Multi card support

The firmware versions with 448 or 896 program steps can read/write up to 4 card sides. This makes it possible to save 448 program steps.

#### Limitations
- **Requires** an x11-calc-67 version that is **under development** (as of October 6, 2025),
- Only 448 program steps can be read/written (2 program cards, 4 sides).
- Only the first 25 registers + I-register can be read/written (1 data card, 2 card sides).


## Versions

### HP67-ext-26-224.rom

Has the standard number of registers and program steps, but implements the indirect X-register functions.

- 26 registers (0-19, A-E, I)  Register I = reg# 25 (Standard HP67)
- 224 program steps (Standard HP-67)
- RCL (x), STO (x), GTO (x)

### HP67-ext-101-448.rom

Extends the number of registers and doubles the program steps.

- 101 registers (0-19, A-E, 25-99, I)  NOTE: Register I = reg# 100
- 448 program steps
- RCL (x), STO (x), GTO (x)
- 2-cards, 4-side support

### HP67-ext-101-896.rom

Extends the number of registers and quadruples the program steps.

- 101 registers (0-19, A-E, 25-99, I)  NOTE: Register I = reg# 100
- 896 program steps
- RCL (x), STO (x), GTO (x)
- 2-cards, 4-side support. Note: can not read/save program steps above 448


## Usage

To start **x11-calc-67** using the 101 register, 448 program step firmware, do:
```
x11-calc-67 -r hp67-extended-101-448.rom -m 256
```
