# 1. What are address bindings in relation to loading a program in memory? 

When we write a program, we normally use variable names and instructions, not the actual memory addresses. But the computer needs real addresses in memory(RAM) to run the program. This process of changing the program’s addresses(variables and data) into real memory addresses is called address binding.

There are three main stages where this binding can happen:

* **Compile time**: If we know in advance exactly where the program will be in memory, the compiler creates code(absolute code) with those fixed addresses.
* **Load time**: If we don’t know the exact memory location in advance, the program is made relocatable(relocatable code). When the program is loaded into memory, the loader adjusts the addresses.
* **Execution time**: Sometimes a program may move around in memory while it runs (for example, in multiprogramming). In that case, the final binding happens while the program is running, with the help of special hardware like the MMU (Memory-Management Unit).

So basically, address binding is about connecting the program’s code and data with the actual memory space where it will run.

---

# 2. Describe the logical vs physical address space. 

When a program runs, the CPU doesn’t directly use the physical memory addresses. Instead, it first works with logical addresses(also called virtual addresses). These are what the program thinks it’s using.

* **Logical address**: Created by the CPU when the program runs. For example, if a program asks for array[10], that’s a logical address.
* **Physical address**: The actual place in the RAM where the data is stored.

The set of all possible logical addresses is called the logical address space, and the set of all possible physical addresses is the physical address space.

The conversion from logical address to physical address is done by the Memory-Management Unit (MMU) and this is a form of execution-time binding. For example, the MMU can take a base value from a relocation register and add it to the logical address to get the physical address.

In short, the user program never accesses the real physical address, the user program only deals with logical addresses, the operating system and MMU map these logical addresses to real RAM locations.

---

# 3. Compare dynamic linking with static linking for shared libraries.

Programs often need functions that are already written in libraries like math functions, printing functions, etc. The way these libraries are connected to the program is called linking.

There are two types of linking:

## Static Linking
* The library code is directly copied into the program’s executable file at compile time.
* Every program has its own copy of the library.

**Pros**: The program can run by itself without needing external libraries at runtime. It may also start faster.  
**Cons**: It makes the program file larger and wastes memory since many programs will have duplicate copies. Also, if the library is updated (e.g., a bug fix), each program must be recompiled.

## Dynamic Linking
* The program doesn’t store the library code inside its executable. Instead, the linking of the library is postponed until execution time.
* At runtime, the program shares the library already in memory.

**Pros**: Saves memory and disk space because many programs share the same library. Also, updating a library automatically updates all programs that use it.  
**Cons**: The program needs the library available at runtime, and starting up might take a little longer.
