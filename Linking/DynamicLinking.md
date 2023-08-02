# Dynamic Linkers (also known as dynamic loaders)

These create executables that rely on separate library files (shared libraries). 
The final binding of the library routine to the executable code is not done until the program is loaded or even during the execution of the program, hence "dynamic". 
This makes executables much smaller and allows them to share libraries, saving system resources.

