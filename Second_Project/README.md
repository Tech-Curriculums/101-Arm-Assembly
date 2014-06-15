BASIC ARITHMETIC
----------------

In this sequence we proceed to create an assembly program that performs basic
arithmetic.

The Raspberry Pi has *only* 16 integer registers (r0 to r15). Each can hold 32 bits.


## Basic idea (sum01.s)

Same procedure as before but we can `add` registers


```arm
/* -- sum01.s - */
.global main
.func main

main:
  mov r1, #3   /* r1 <- 3 */
  mov r2, #4   /* r2 <- 4 */
  add r0,r1,r2 /* r0 <- r1 + r2 */
  bx lr
```

## Reusing Registers (sum02.s)

Look into the `advanced` folder and look at the same code now reusing your scarce registers.

``arm
/* -- sum02.s - */
.global main
.func main

main:
  mov r0, #3   /* r0 <- 3 */
  mov r1, #4   /* r1 <- 4 */
  add r0,r0,r1 /* r0 <- r0 + r1 */
  bx lr

```
