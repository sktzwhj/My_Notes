#Programming Language
##C++
###locks

####exclusive lock 
互斥锁在被阻塞时CPU可以运行其他程序，这一点主要是和自旋锁区分开来。

####spinning lock
自旋锁适用于短时间轻量级的锁。

####condition lock
用来等待一个条件，pthread_cond_wait(cond, mutex)

具体到C++11中
exclusive lock可以用unique_lock实现。

读写锁可以用shared_lock实现，shared_lock被用于保护频繁读取但是写入很少的数据结构。读取时用lock_shared()进行加锁而写入时用lock()进行加锁。读者互相读时无需互斥，而写者需要与其他线程互斥。