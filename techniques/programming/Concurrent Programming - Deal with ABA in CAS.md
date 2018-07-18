#Deal with ABA problem in CAS

When we are building lock-free data strcutures, ABA is a typical problem if CAS (compare-and-set) is used. Let's take stack as an example, if one thread changes the top of the stack and change it back to the original value, some threads may think the value is not changed and update its value. 

This problem happens because we only check the value. 

Solutions to deal with ABA prblem:
1. add a version tag. but the problem is that you need to fit both the pointer and the tag in the length of a pointer. for example, you can make the pointer shorter (i.e., ensure that the length of the list is limited). or you can use anohter primitive called linked-load/store-conditional. But it seems it is only supported by ARM rather than x86 for now.

some important concepts,
1. obstruction-free, lock-free, wait-free?

generally, lock-free must be obstruction-free and wait-free must be lock-free.
obstruction-free guarantees the execution time of a single thread while wait-free guarantees the execution time system-widely. 