# Low-level Computing

## Alignment

The purpose is minimizing CPU read cycles

Data is said to be _naturally aligned_ if data's memory address is a multiple of the data size.

_Data alignment_ is the aligning of elements according to their natural alignment, which may require
some _padding_ between elements.

Padding is only inserted when a structure member is followed by a member with a larger alignment 
requirement or at the end of the structure.

>For example, on a 32-bit machine, a data structure containing a 16-bit value followed by a 32-bit 
>value could have 16 bits of padding between the 16-bit value and the 32-bit value to align the 
>32-bit value on a 32-bit boundary.

A memory access is _aligned_ when the data being accessed is n bytes long and the datum address 
is n-byte aligned (multiple of n).

A memory pointer that refers to primitive data that is n bytes long is aligned if it is only 
allowed to contain addresses that are n-byte aligned.

A memory pointer that refers to a data aggregate (a data structure or array) is aligned if 
(and only if) each primitive datum in the aggregate is aligned.

_Packing_ a structure means omitting padding between elements.
