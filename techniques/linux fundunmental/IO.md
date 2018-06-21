#Linux Kernel I/O
##File I/Os
pipe - a buffer in kernel space which can be used in the communication between processes. 

(1) a pipe is actually implemented by having a virtual file descriptor between two processes. One write to the file while the other read from it. 

(2) the max number of opened files in typical linux system is 1024 while you can set it up to around 1 million.

(3) the round-robin async I/O is basicly implemented in the following way:
the process firstly tries to read/write and an error code returns and the processes decide what to do according to the error code. it is obviously inefficient. 

About edge-triggered or level-triggered, the following gives a good explanations
https://www.cnblogs.com/liloke/archive/2011/04/12/2014205.html

##Buffered I/Os

The Linux kernel has system calls like open(), close(), write(), ...
In practice, when we are implementing I/Os, we normally use the glibc library implementation in the user space rather than call the system calls directly. The standard I/O routines in glibc uses file pointers rather than file descriptors, although those two are mapped inside the glibc library. 

The glibc-implemented I/O operations implement the buffer in the user space. Sometimes it may not help a lot since you have file-system level buffer implemented in the kernel. Developers can set the size and buffer/or not by setvbuf().

Although each operation is atomic and thread-safe for buffered I/O implementations, users would need to use the file lock APIs to guarantee different-grained critic zone. 

The main problem for buffered I/O is the double copy problem which can be solve in some way or by better I/O libs. 

The motivations for users to use buffered I/O rather than system calls (file I/Os):
1. avoid issue many system calls
2. ensure block-sized chunks and block-aligned boundaries
3. access pattern is character- or line based

##Advanced File I/Os
###Scatter/Gather I/Os
functions like readv() and writev() can read/write several segements at the same time and guarantee the atomity.  

###The Event Poll Interface
http://devarea.com/linux-io-multiplexing-select-vs-poll-vs-epoll/#.Wys3rnWWbJ8
The above link gives very good examples showing the differences between epoll and pool, select. Note that epoll is a Unix-specific thing and not as portable as select and pool. 