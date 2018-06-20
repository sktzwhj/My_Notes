#Linux Kernel I/O

pipe - a buffer in kernel space which can be used in the communication between processes. 

(1) a pipe is actually implemented by having a virtual file descriptor between two processes. One write to the file while the other read from it. 

(2) the max number of opened files in typical linux system is 1024 while you can set it up to around 1 million.

(3) the round-robin async I/O is basicly implemented in the following way:
the process firstly tries to read/write and an error code returns and the processes decide what to do according to the error code. it is obviously inefficient. 

About edge-triggered or level-triggered, the following gives a good explanations
https://www.cnblogs.com/liloke/archive/2011/04/12/2014205.html
