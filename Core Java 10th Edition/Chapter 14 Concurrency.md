# Chapter 14

## Threads
- Using threads
```
Runnable r = () -> {task code;};
Thread t = new Tread(r);
t.start();
```
- Interrupting threads
```
Runnable r = () -> {
    try {
        ...
        while (!Thread.currentThread().isInterrupted() && more work to do) {
            do more work
        }
    } catch (InterrruptedException e){
        // thread was interrupted during sleep or wait
    } finally {
        cleanup, if required
    }
    // exiting the run method terminates the thread
}
```
- Daemon Threads
    - When only daemon threads remain, the virtual machine exits.
    - Should never access a persistent resource sucha as a file or database since it can terminate at any time, even in the middle of an operation.

## Synchronization
- ReentrantLock
```
private Lock myLock = new ReentrantLock();

myLock.lock();
try {
    critical section
} finally {
    // make sure the lock is unlocked no matter what happens
    myLock.unlock();
}
```
- Condition Objects
```
class Bank {
    private Condition sufficientFunds;
    ...
    public Bank() {
        ...
        sufficientFunds = bankLock.newCondition();
    }
    
    public void transfer(int from, int to, int amount) {
        bankLock.lock();
        try {
            while (accounts[from] < amount)
                sufficientFunds.await();
            // transfer funds
            ...
            sufficientFunds.signalAll();
        } finally {
            bankLock.unlock();
        }
    }
}
```
- The ```synchronized``` Keyword
```
public synchronized void method(){
    // method body
}

// is equivalent to 

public void method() {
    // Every object has an intrinsicLock
    this.intrinsicLock.lock();
    try {
        // method body
        
        // equivalent to intrinsicCondition.await();
        wait();
        
        // equivalent to intrinsicCondition.signalAll();
        notifyAll();
    } finally {
        this.intrinsicLock.unlock();
    }
}
```
- Limitation of intrinsic lock and condition
    - You cannot interrupt a thread that is trying to acquire a lock.
    - You cannot specify a timeout when trying to acquire a lock.
    - Having a single condition per lock can be inefficient.
- What to use
    - It is best to use neither Lock/Condition nor the ```synchronized``` keyword. Use classes in java.util.concurrent instead.
    - If ```synchronized``` keyword works for your situation, use it.
    - Only when none of the above solution works, consider using Lock/Condition.
- Synchronized Blocks
    - Client-side locking
    - Generally not recommended because it relys on the correct implementation of client side code 
```
// will acquire the lock for obj
synchronized (obj) {
    critical section
}
```
- ```volatile``` Fields
    - Disable cache in CPU and reorder of instructions by compiler.
    - The change of the field made by one thread is guaranteed to be seen by another thread.
    - But no atomicity guarantee.
- Atomics

## Blocking Queues
- LinkedBlockingQueue
- ArrayBlockingQueue
- PriorityBlockingQueue
- DelayQueue
- TransferQueue (interface)

## Thread-Safe Collections
- ConcurrentHashMap
- ConcurrentSkipListMap
- ConcurrentSkipListSet
- ConcurrentLinkedQueue
