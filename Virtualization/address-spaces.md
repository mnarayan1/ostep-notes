## Address Spaces

Problem 1: Cannot have one program taking up the rest of OS memory, and context switch each time

Problem 2: Cannot know address space of other processes

Address space
- Running program's view of the memory in the system
- Contains code (top), stack (bottom growing up), and heap (below code growing down)

This is virtualizing memory (mfw they use the word virtualizing AGAIN)

Static allocation (moving address by a fixed amount) is really insecure and hard to relocate address space to another location.

Dynamic (hardware-based) Relocation
- Base and bound register allows us to place address space anywhere we'd like in phyysical memory
- Decide where in physical memory should be loaded and set base to that value
- Before referencing memory, check to see if it's in bounds
- MMU helps with address translation

physical add = virtual + base

What does OS do
- Look in physical memory to see where we can put process (free list, similar to malloc?)
- Exit process by reclaiming memory
- Must save base and bounds pair each time it switches between processes
- Provide exception handlers to terminate processes

Problems: memory fragmentation