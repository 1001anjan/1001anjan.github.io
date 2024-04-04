---
layout: default
title: Hazelcast Lock
parent: Hazelcast
nav_order: 8
---
# Hazelcast Lock
Hazelcast is an in-memory data grid (IMDG) solution that provides distributed data structures and services, allowing applications to scale out across multiple nodes and handle large volumes of data with high throughput and low latency.

One of the features provided by Hazelcast is the distributed locking mechanism. A distributed lock in Hazelcast allows you to synchronize access to a shared resource across multiple nodes in a cluster. Here are some key points about Hazelcast locks:

1. Distributed Nature: Unlike local locks which are confined to a single JVM (Java Virtual Machine), Hazelcast distributed locks work across multiple JVMs and nodes in a Hazelcast cluster. This ensures that the lock state is consistent across the entire cluster.
2. Reentrant Locks: Similar to Java's ReentrantLock, Hazelcast provides reentrant distributed locks. A reentrant lock allows the same thread to acquire the lock multiple times without causing a deadlock.
3. Lock Timeout: You can specify a timeout for acquiring a lock. If a lock cannot be acquired within the specified timeout period, Hazelcast will throw a LockAcquireLimitReachedException.
4. Auto-release Locks: Hazelcast provides the option to automatically release a lock after a specified lease time. This is useful to prevent potential deadlocks in case a node holding the lock becomes unresponsive.
5. Fair vs. Non-fair Locks: Hazelcast supports both fair and non-fair locking mechanisms. In a fair locking system, locks are granted in the order in which they were requested (first-come, first-served). In a non-fair system, there is no guaranteed order.

Here's a simple example of how you might use a Hazelcast distributed lock in Java:
```java
public class DistributedCacheServiceImpl {

    private final HazelcastInstance hazelcastInstance;

    DistributedCacheServiceImpl(HazelcastInstance hazelcastInstance) {
        this.hazelcastInstance = hazelcastInstance;
    }
    
    public boolean executeWithLock(String lockName, Runnable criticalSection) {
        FencedLock lock = hazelcastInstance.getCPSubsystem().getLock(lockName);
        boolean lockAcquired = false;

        try {
            lockAcquired = lock.tryLock();

            if (lockAcquired) {
                try {
                    log.info("Locking the job for execution. LockName: {}",lockName);
                    criticalSection.run();
                    return true;
                } catch (Exception e) {
                    // Handle exceptions thrown in the critical section
                    log.error("Error in critical section: {}", e.getMessage(), e);
                    return false;
                }
            } else {
                log.error("Lock not acquired. Skipping execution for lock name {}", lockName);
                return false;
            }
        } finally {
            if (lockAcquired) {
                try {
                    lock.unlock();
                } catch (Exception e) {
                    // Handle exceptions thrown during unlock
                    log.error("Error while unlocking: {}, {}, ", lockName, e.getMessage(), e);
                }
            }
        }
    }
    
    public boolean acquireLock(String lockName, long timeoutMillis) {
        FencedLock lock = hazelcastInstance.getCPSubsystem().getLock(lockName);

        try {
            return lock.tryLock(timeoutMillis, java.util.concurrent.TimeUnit.MILLISECONDS);
        } catch (Exception e) {
            e.printStackTrace();
            return false;
        }
    }
    
    public void releaseLock(String lockName) {
        FencedLock lock = hazelcastInstance.getCPSubsystem().getLock(lockName);

        try {
            lock.unlock();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```