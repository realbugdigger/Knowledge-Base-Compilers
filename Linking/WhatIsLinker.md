# What is a linker?

A linker is a computer program that takes one or more object files generated by a compiler and combines them into a single executable program.
Computer programs are often made of multiple modules that can be compiled separately. 
This allows programmers to build applications from reusable pieces of code. 
However, these modules have to be combined into a single executable before they can be run. 
This is where the linker comes in.

There are two main types of linkers:
- Static Linkers: These create standalone executables. All library routines used by the program are copied into the executable. While the resulting file can be larger, it can also be run on any compatible system regardless of the libraries it has installed.
- Dynamic Linkers (also known as dynamic loaders): These create executables that rely on separate library files (shared libraries). The final binding of the library routine to the executable code is not done until the program is loaded or even during the execution of the program, hence "dynamic". This makes executables much smaller and allows them to share libraries, saving system resources.

In summary, a linker takes smaller object files and combines them into a single continuous program that can be loaded and executed. It resolves references between these object files, replacing placeholders from each object file with the correct addresses, based on the combined size of the various modules.


