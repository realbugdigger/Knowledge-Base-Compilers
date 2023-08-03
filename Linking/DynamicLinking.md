# Dynamic Linkers (also known as dynamic loaders)

These create executables that rely on separate library files (shared libraries). 
The final binding of the library routine to the executable code is not done until the program is loaded or even during the execution of the program, hence "dynamic". 
This makes executables much smaller and allows them to share libraries, saving system resources.

## Implicit Linking vs Explicit Linking

Dynamic linking occurs differently based on whether shared libraries are loaded implicitly at load time (static linking) or explicitly at runtime.

### Implicit Linking (Load-Time)

Implicit linking, also known as load-time dynamic linking, occurs when a program is loaded into memory before its execution begins. The executable references a symbol (variable or function) in a dynamic shared library. This referencing is resolved by the dynamic linker at load time.

Here are the steps:

1. When you start the program, the dynamic linker is invoked.
2. The dynamic linker examines the program to find any dynamic libraries the program needs before it can run.
3. The linker then loads these libraries into memory, if they aren't loaded already.
4. After loading the libraries, the linker updates all references in the program to point to the correct locations where the shared libraries are loaded in memory.

### Explicit Linking (Run-Time)

Explicit linking, also known as run-time dynamic linking, allows a program to decide when to load and unload libraries during its execution.

Here are the steps:

1. The program contains specific code that calls system routine functions (like dlopen, dlclose, dlsym, etc., in Unix-like systems). These routines load and unload shared libraries as well as locating symbols.
2. With the dlopen call, the program loads a shared library into memory during runtime.
3. Using the dlsym function, the program obtains the address of a symbol (like a function or variable) in the shared library.
4. The program can now directly call a function in the shared library using this address.
5. When it is done with a library, the program will unload it from memory with the dlclose call.


The difference between explicit and implicit linking lies in flexibility versus simplicity. 
Explicit dynamic linking provides the program with more direct control over its shared libraries but requires writing additional code to handle the loading, linking, and unloading processes. 
Implicit dynamic linking handles all this automatically at the cost of flexibility.

