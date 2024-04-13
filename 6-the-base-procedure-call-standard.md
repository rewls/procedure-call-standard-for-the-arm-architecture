# 6 The Base Procedure Call Standard

- The base standard defines a machine-level, core-registers-conly calling standard common to the Arm and Thumb instruction sets.

- It should be used for systems where there is no floating-point hardware, or where a high degree of inter-working with Thumb code is required.

## 6.1 Machine Registers

- The Arm architecture defines a core instruction set plus a number of additional instructions implemented by co-processors.

- The core instruction set can access the core registers and co-processors can provide additional registers which are available for specific operations.

### 6.1.1 Core registers

- There are 16, 32-bit core (integer) registers visible to the Arm and Thumb instruction sets.

- These are labeled r0-r15 or R0-R15.

- Register names may appear in assembly language in either upper case or lower case.

- In this specification upper case is used when the register has a fixed role in the procedure call standard.

> ##### Core registers and AAPCS usage
>
> |Register|Synonym|Special|Role in the procedure call standard|
> |-|-|-|-|
> |r15||PC|The Program Counter.|
> |r14||LR|The Link Register.|
> |r13||SP|The Stack Pointer.
> |r12||IP|The Intra-Procedure-call scratch register.|
> |r11|v8|FP|Frame Pointer or Variable-register 8.
> |r10|v7||Variable-register 7.|
> |r9|v6|SB<br>TR|Platform register or Variable-register 6.<br>The meaning of this register is defined by the platform standard.|
> |r8|v5||Variable-register 5.|
> |r7|v4||Variable-register 4.|
> |r6|v3||Variable-register 3.|
> |r5|v2||Variable-register 2.|
> |r4|v1||Variable-register 1.|
> |r3|a4||Argument / scratch register 4.|
> |r2|a3||Argument / scratch register 3.|
> |r1|a2||Argument / result / scratch register 2.|
> |r0|a1||Argument / result / scratch register 1.|

- The first four register r0-r3 (a1-a4) are used to pass argument values into a subroutine and to return a result value from a function.

    - They may also be used to hold intermediate values within a routine (but, in general, only *between* subroutine calls).

- Register r12 (IP) may be used by a linker as a scratch register between a routine and any subroutine it calls (for details, see Use of IP by the linker).

    - It can also be used within a routine to hold intermediate values between subroutine calls.

- In some variants r11 (FP) may be used as a frame pointer in order to chain frame activation records into a linked list.

- The role of register r9 is platform specific.

    - A virtual platform may assign any role to this register and must document this usage.

    - It may designate it as the static base (SB) in a position-independent data model.

    - It may designate it as the thread register (TR) in an environment with thread-local storage.

- Typically, the registers r4-r8, r10 and r11 (v1-v5, v7 and v8) are used to hold the values of a routine's local variables.

- A subroutine must preserve the contents of the registers r4-r8, r10, r11 and SP.

- In all variants of the procedure call standard, registers r12-r15 have special roles.
