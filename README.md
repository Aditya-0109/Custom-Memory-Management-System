# MeMS: Memory Management System
MeMS is a custom memory management system implemented in the C programming language. It utilizes system calls mmap and munmap for memory allocation and deallocation, respectively. MeMS aims to provide efficient memory management while adhering to specific constraints and requirements outlined below.

**Constraints and Requirements**

MeMS solely utilizes the system calls mmap and munmap for memory management. The use of other memory management library functions such as malloc, calloc, free, and realloc is strictly prohibited.
Memory allocation requests are made in multiples of the system's PAGE_SIZE, determined using the command getconf PAGE_SIZE.
Memory deallocation occurs only through munmap, and deallocation sizes are in multiples of PAGE_SIZE.
The PAGE_SIZE macro is used to ensure compatibility across systems.
User programs must use MeMS functions for memory allocation and deallocation, with the use of other memory management library functions disallowed.
MeMS maintains a free list data structure to track allocated and unallocated memory, consisting of processes and holes.
Free List Structure
The free list is represented as a doubly linked list, comprising main chains and sub-chains. Main chains correspond to memory regions allocated by MeMS, while sub-chains represent segments within these regions.

**Main Chain Features:**

New nodes are added to the main chain when memory is allocated using mmap.
Each main chain node points to a sub-chain, which contains segments of allocated and unallocated memory.
Sub-Chain Features:

Segments represent portions of memory, categorized as either processes (mapped to user programs) or holes (unallocated).
Holes can be reallocated, with any remaining space creating new hole segments in the sub-chain.
MeMS Virtual Address and MeMS Physical Address
MeMS virtual addresses are utilized for memory allocation within the MeMS virtual address space. These addresses are mapped to MeMS physical addresses, which are provided by mmap.

MeMS maintains a mapping from virtual address space to physical address space, allowing user processes to interact with heap memory via MeMS virtual addresses.
