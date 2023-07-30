# PL-ideas
1. No implicit stack
Functions would have a frame data type.  If you call a function, then your frame will contain enough space to hold that function's frame.  This means that you can't call your function recursively.  Instead, you would need to dynamically allocate a function frame - handle any out-of-memory errors - and then call it.
Function frames should be able to be allocated anywhere.  Somehow, you should be able to re-enter a function frame multiple times, and this should somehow map to generators / futures / coroutines / etc.
2. Only one numeric type: arbitrary-precision, signed, integers
Floats are just a pair of integers.  Unsigned integers are just integers with a constraint.  u8 storage class is just an integer with two constraints. etc.  The integers should also be able to function as bit vectors.
3. Constraint solver
Have an unreachable keyword.  The unreachable keyword should result in a compilation error if the compiler cannot prove that it is in fact impossible to reach.  This is how constraints would be added to the integers: `if (i < 0) { unreachable }` would mean that i must be an unsigned integer.  `if (i.bitlength > 64) { unreachable }` would mean that i must be an i64.
4. Constant time constraints
In addition to the numeric constraint solver, there should be a constant time block:
`#[constant_time]
{
	if (i < 4) { }
	else { }
}
`
This would tell the compiler to ensure that all possible execution paths in this block take the same amount of time.  If this isn't possible, then that should be a compiler error.
5. Interpreted
The language should be interpreted, but with a compiler inside the standard library.  There would be enough introspection that the compiler library can generate code from first-class functions.  This way you don't need a build system: you write a program that outputs artifacts.
6. Multiple artifacts
Modern languages are expected to output executables, documentation, run tests, etc.  I would like it to be possible to design a CPU in the language.  That is you could write code that outputs hardware descriptions, validates things, and outputs various emulator binaries.  Code is just data.  You should be able to compile the same code to multiple different ISAs and then compose those instruction streams into the same binary to support writing complex firmware.
7. No pointers: preferably
I would prefer to not have pointers.  I don't know how this would work with dynamic dispatch / trait objects / 
