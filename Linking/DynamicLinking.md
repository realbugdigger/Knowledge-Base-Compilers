# Dynamic Linkers (also known as dynamic loaders)

These create executables that rely on separate library files (shared libraries). 
The final binding of the library routine to the executable code is not done until the program is loaded or even during the execution of the program, hence "dynamic". 
This makes executables much smaller and allows them to share libraries, saving system resources.

## High-level view of how dynamic linking works

Dynamic linking is a process that happens at the time of execution. It's a mechanism that connects an executable program with the shared libraries it needs to run. The central component of this process is the dynamic linker (or dynamic loader). Here's a high-level view of how it works:

1. **Loading**: When a program that uses shared libraries is executed, the system first loads the dynamic linker. The role of the dynamic linker is essentially to prepare the program to run. It loads the executable into memory and determines which shared libraries are needed by the program.

2. **Linking**: The dynamic linker then locates the necessary shared libraries (if they are not already loaded into memory) and maps them into the program's address space. When the libraries are loaded into memory, the dynamic linker connects the executable and the shared libraries, supplying the addresses where the shared libraries exist in memory. 

3. **Relocation**: "Relocation" is the process of adjusting absolute references between the loaded executable and the shared libraries. For every reference to a function or variable from the shared library, the dynamic linker redirects the calls or references via a look-up table like the Global Offset Table (GOT) to the actual memory addresses of the needed functions or variables.

4. **Resolution**: In some cases, multiple libraries may contain a definition for a certain symbol. The dynamic linker resolves symbol conflicts as well. It uses a set of rules, known as the symbol resolution rules, to determine which of the potential symbols to use. Note that the way the dynamic linker handles symbol resolution may depend on the specific operating system and linker used.

When all dynamically linked shared libraries are loaded and all references are resolved, the dynamic linker jumps to the startup routine of the loaded program to begin execution. This entire process is transparent to the end-user, and the program executes as if it was one self-contained binary.

One major advantage of dynamic linking is that it allows multiple programs to share the same library code. This conserves system storage and memory, as the same code doesn’t need to be present in multiple places in memory. Any updates or fixes to shared libraries can be applied without having to modify or recompile the dependent programs. However, it also means that dynamically linked programs must have access to the libraries they depend on in the correct versions so they can function correctly.

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

## PLT and GOT

### Procedure Linkage Table (PLT)

The PLT is used to call external functions whose address isn't known in the time of linking, and is left to be resolved by the dynamic linker at run time..

When a program calls a function that belongs to a shared library, the control is passed to the PLT entry of that function. This PLT entry then passes on the control to the appropriate function in the shared library.

### Global Offset Table (GOT)

It works hand-in-hand with the PLT to facilitate dynamic linking.

The PLT makes use of the GOT to find out the address of the function or variable it needs to access. The linker fills the GOT entries with the addresses of variables or functions that the program must access during runtime.

When a dynamically linked library is loaded/unloaded during the execution of a program, only the GOT is updated with the new addresses of the entities (variables or functions). This allows the actual code to remain in place without needing to be updated with the new addresses, hence allowing better efficiency and modularity in handling shared libraries.

To sum it up, the Procedure Linkage Table (PLT) and Global Offset Table (GOT) are mechanisms used by the system to handle external functions and variables in a modular and efficient way while executing a dynamically linked program or library.

### Example

When you call puts() in C and compile it as an ELF executable, it is not actually puts() - instead, it gets compiled as puts@plt. 

Why does it do that?

Well, as we said, it doesn't know where puts actually is - so it jumps to the PLT entry of puts instead. 
From here, `puts@plt` does some very specific things:
- If there is a GOT entry for `puts`, it jumps to the address stored there.
- If there isn't a GOT entry, it will resolve it and jump there.

The GOT is a *massive* table of addresses; these addresses are the actual locations in memory of the `libc` functions. `puts@got`, for example, will contain the address of `puts` in memory. 
When the PLT gets called, it reads the GOT address and redirects execution there. 
If the address is empty, it coordinates with the `ld.so` (also called the **dynamic linker/loader**) to get the function address and stores it in the GOT.

https://ir0nstone.gitbook.io/notes/types/stack/aslr/plt_and_got

https://www.technovelty.org/linux/plt-and-got-the-key-to-code-sharing-and-dynamic-libraries.html

https://www.geeksforgeeks.org/linker/

