Hello Arm Assembly
------------------

Assembly is a little more involved than other types of languages, so we will start real simple.

In this program you will create a program which returns a number.


We will also discuss the basics of creating a makefile.

## The Program

The following arm assembly program simply puts the number `4` in the register `r0`

```arm
/* -- first.s */
/* This is a comment */
.global main /* 'main' is our entry point and must be global */
.func main   /* 'main' is a function */
 
main:          /* This is main */
    mov r0, #4 /* Put a 2 inside the register r0 */
    bx lr      /* Return from main */
```


#### C0d3 Breakdown

Basically you have a global entry point, which turns out to be a function.
```arm
.global main /* 'main' is our entry point and must be global */
.func main   /* 'main' is a function */
```

That function places a `4` in register r0 and then returns:

```arm
main:          /* This is main */
    mov r0, #4 /* Put a 2 inside the register r0 */
    bx lr      /* Return from main */
```

## The Makefile

Makefiles accelerate the command line build process (over a simple shell script), and require less typing (faster execution).

```
all: first

first: first.o
	gcc -o $@ $+

first.o : first.s
	as -o $@ $<

clean:
	rm -vf first *.o
```

* `all: first`  -- when you type in `make all` it will look for the line that starts with `all:` and start
building the prerequisites (in this case `first`).  BUT first has prerequisites (`first.o`), which has prerequisties, and so forth...  going far enough down the prerequisite chain, it find something it can build, and works itself back up and actually build what you asked.
	* Efficiency -- trust me it sounds complicated, but Makefiles are specially designed to execute quickly and utilize multiple cores. IN OTHER WORDS, it'll be very *fast*.
* `$@`  -- an abbreviation for the "target" -- the thing left of the colon `:`
	* Example: `first: first.o` first is the target (to the right of the colon, we have "prerequisites")
* recipe  -- this is what you do with target and prerequisites.  E.G. `gcc -o $@ $+ ` compiles the target ($@) with all of the prerequisites ($+).

