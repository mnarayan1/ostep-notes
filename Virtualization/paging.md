## Paging

Rather tha aplitting address space into logical segments, we divide process address space into fixed-size units called **pages**. View physical memory as an array of slots called **page frames**.  

Record where each virtual page of the address space is placed in a page table. Each process has a page table.

Virtual address has 6 bits
- Virtual page number (va5, va4) (n)
- Offset (va3-va0)

Get the page frame of the nth entry in the page table, and load that page.

Page Table
- Gets big, so we store it in physical memory that OS manages
- Entry: valid bit indicates whether translation is valid. Unused space in ebtween marked as invalid
- Protection bit indicates page permissions

### TLBs
Speed up address translation => cache of popular virtual to physical address translations

Upon virtual translation, it's held in TLB.
1. Extract VPN from virtual address
2. Check if TLB has translation from this => if TLB hit, extract page frame number, form PA and access memory
3. If TLB Miss, add TLB, retry instruction, memory processed

## Swapping
What if your process is bigger than the address space provided? Only parts of the program will be loaded into memory. Only some addresses will be in TLB. If not, there will be page fault.

Full workflow
1. Extract VPN from virtual address, check TLB for a match
2. If not in TLB (TLB miss), look up page table in memory, then add to TLB
3. Present bit added to page table entry to check if it is present in physical memory: 1 if it is, zero if elsewhere (if not in physical memory, called a **page fault**)

Handling page faults: find page in secondary storage (hard drive, ssd), load it into free frame in RAM, update page table and TLB, resume program

Swapping: Identify inactive/less-used RAM and moves it to swap space if there is not enough RAM