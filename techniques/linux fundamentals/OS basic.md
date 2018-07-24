#Operating Systems Notes for Berkerly CS 162 - process, thread and address spaces

Recap some concepts to prepare my tutoring.

##L02

process - unit of resource allocation and execution

thread - unit of execution

each thread should have their own PC, SP (stack pointer) and registers

hyperthreading techniques can help to improve the performance by making the context switch for threads faster. They replicate some hardware like pc and registers to achieve this. 

how to protect threads from one another. 
1. protection of memory
2. protection of I/O devices
3. Protection of access to processor

each process has their own page table. 

process: operating system abstration to represent what is needed to run a single program. 

it contains two parts, sequential program execution stream and protected resources (memory aka. the page table, I/O states e.g., file descriptors).

there is no concurrency in a heavyweight process.

how to multiplex processes?

There is process control block which contains the process state, process number, pc, registers, memory limits, limits of open files... for each process.

Give out CPU time to different processes (scheduling)
- only one process runing at a time
- high-priority processes get more resources. 

For a context switch, we need to save the state of one process to PCB and reload the state of another process to PC, registers, file discriptor table, etc. 

The kernel code finishing this procedure is kinda overhead. The overhead will be less under the architecture of SMT/Hyperthreading since they have extra hardwares to reduce the stats.


Processes need to communicate. - shared memory or message passing (send, receive or pipe)

shared memory - really low overhead but introduces complex sychronization problems. 

inter-process communications (IPC)

Modern 'lightweight' process with threads
threads have their own registers and stack. they share code, data and files. 

##L03 Concurrency and Thread Dispatching
Why Process & Threads
Goals: Multiprogramming and Protection

Solution:
1. Process - virtual machine abstraction - give process illusion it owns machine
challenge - process creation and switching is expensive
and we also need concurrency within the same app

thread context switching is faster than process switching since you do not have to switch some parts of the process. e.g., address space. and when there are multiple cores, you do not need to switch the registers, etc. because different threads are running on different physical cores. 

Actually, the state-of-the-art difference between single-threaded process and thread context switching is much smaller. (process - 3-4us, 100ns) Reason? - cache. That's why switching across cores would be much slower. 

The context switching time increases sharply with the size of the working set, and can increse 100x or more. working set means the memory locations which the process often hits. 

Caveat - many process are multi-threaded so a typical process context switch may be in fact many thread context switches. 

State shared by all threads in a process - content in memory and I/O state. 

Each thread privately own TCB, CPU registers and execution stack 
what is exeuction stack - parameters, temporary varaibles, return pcs, etc. 

for example, for each function call, we need to have an address for stroing the returning address after the function finishes. 

Per thread state includes CPU registers, program counter and pointer to stack (SP). also the scheduling info used by the OS. and various pointers to the different thread status queue which are used for scheduling as well.

There are different queues - i.e., ready queue
except the ready queue, we also have various I/O device queues for I/O devices. in the queue, the elements are also the TCB. 

Running a thread.
load its state, load environment, jump to the PC. 

Apart from timer, interrput, etc, there are also system calls which allow a thread to **yield** by itself. 

In fact, in Linux, a piece of user stack and a kernel stack. 
for example, a yield actually calls for an interrupt which later calls the kernel_yield. 

Finished threads not killed right away. for latency consideration.

For programs which do not have yield. TimerInterrupt solves the problem even if the user does not insert yield by themselves. 

Use the multi-thread web server as an example. If you have unbounded number of threads, the system throughput will sink when it becomes popular. So the solution can be using thread pool. The number of threads in the thread pool represents the max level of multiprogramming. 

Questions. User level thread and kernel level thread. 
User level threads are normally implemented by a user library. 

Can a user level thread uses more than one cpu core?
Theoriotically, user level threads can only run in the same core. But if some implementations are using native thread supports, it is possible that they are scheduled to run on different cores. 

##L04 Sychronization, Atomic Operations and Locks

How can we actually implement a lock 

Acquire() {
disable interrupts;
if (value == BUSY) {
	put thread on wait queue;
    go to sleep();
   	//enable interrupts?
    //how can we enable interrputs after sleep? actually, this is for the next thread which wakes up to turn on the interrupts. 
} else {
	value = BUSY;
}
enable interrupts;
}

Release() {
//disable interrupts;
if(anyone on wait queue) {
take thread off wait queue and put at front of ready queue;
//that means you are the next thread to be weakn to run. 
} else {
	value = FREE;
}
enable interrupts;
}

the value we are talking about here is just the mutex in the programming language. 

 