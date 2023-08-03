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

## Internal linking vs external linking

Internal linking and external linking refer to the process of converting symbolic references into addresses and assigning memory to those symbols or variables in a program.

Let's look at each type in more detail.

### Internal Linking

Internal linking usually refers to the resolution of symbol references within one compilation unit or module.

During the compile stage, the compiler turns your code into an intermediate object file, resolving any references that it can. This includes function and variable references within the same source file.

For instance, if a function funA() calls another function funB() in the same source file, then the compiler internally links funB() when it compiles funA()—that is, funA() knows how to call funB(). This process is why all functions and global/static variables in the same compilation unit or module must have unique identifiers.

### External Linking

External linking usually refers to the resolution of symbol references between multiple compilation units or modules.

After the source files have been internally linked and compiled into object files, they still may contain references to functions or variables defined in other object files. This is where the linker comes in. The linker's job is to stitch together several object files into a single executable. It does this by resolving the symbols that are unknown at compile time—i.e., those defined in other compilation units or modules—and 'patching' the object files together into a complete executable program.

For example, if function funX() defined in one source file File1 calls a function funY() defined in another source file File2, then the external linker is responsible for providing the correct reference of funY() to funX() at link time.

```
In conclusion, internal linking is about resolving references within the same source file during the compilation process,
while external linking is about resolving references between different source files during the linking process.
```

