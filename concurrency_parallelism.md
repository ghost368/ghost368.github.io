
* Think of threads as processes that share the same address space and can access the same memory. Communication is done by shared variables. Multiple threads can run within the same process.
* Processes (in this context, and roughly speaking) have their own private data and if two processes want to communicate that communication has to be done more explicitly.
When you are writing a program where the bottleneck is CPU cycles, neither threads or processes will give you a speedup on a single core machine.
* Processes and threads are still useful for multitasking (rapid switching between (sub)programs) - this is what your operating system does because it runs far more processes than you have cores.

* Processes and threads (or even coroutines!) can give you considerable speedup even on a single core machine if the tasks you are executing are I/O bound - think of fetching data from a network. For example, instead of actively waiting for data to be sent or to arrive, another process or thread can initiate the next network operation.

* Threads are preferable over processes when you don't need explicit encapsulation due to their lower overhead. For most CPU-bound concurrent problems, and especially the large subset of "embarassingly parallel" ones, it does not make much sense to spawn more processes than you have processors.

* The Python GIL prevents two threads in the same process from running in parallel, i.e. from multiple cores executing instructions literally at the same time.

* Therefore threads in Python are relatively useless for speeding up CPU-bound tasks, but can still be very useful for I/O bound tasks, because blocking operations (e.g. waiting for network data) release the GIL such that another thread can run while the other waits.

* If you have multiple processors, you can have true parallelism by spawning multiple processes despite the GIL. This is only worth it for CPU bound tasks, and often you have to consider the overhead of spawning processes and the communication cost between processes.

----------------


* So both threads and processes can be used with single core (via switching, which has limited potential for speed up unless it comes from I/O operations lag) and multiple cores.
* What's important is just that processes have independent memory while threads share the same memory
* It's easier for OS to lauch multiple threads rather then spawn or fork multiple processes
* On multicore multiple threads can work on different CPUs simultaneously


------------------

* A program can be network bound (lag in each I/O operation) or CPU bound (can only benefit from multiple physical cores)

* Threading tools in python cannot be used for parallel computations on multiple CPUs, but work well for I/O bound operations

* GIL does not restrict from having multiple threads - only requires that only one thread is active at a given moment in time

* threading is a standard module in Python (but useful only for I/O bound tasks)
