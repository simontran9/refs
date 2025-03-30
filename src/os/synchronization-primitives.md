# Synchronization primitives

## Mutual exclusion lock

## Condition variable

### `cond_var.notify_one()`

Wakes up at least one of the threads that are currently blocked on the specified condition variable `cond_var`

### `cond_var.notify_all()`

Wakes up all threads currently blocked on the specified condition variable `cond_var`

### `cond_var.wait(mutex)`

1. Atomically releases mutual exclusion lock `mutex`
2. Block on condition variable `cond_var`
3. Wait for a signal from another thread on `cond_var`
4. When signaled/awakened by another thread, attempt to reacquire `mutex`. However, if another thread acquires `mutex`, then the signaled thread blocks, but this time, it's waiting for `mutex` (not for the `cond_var`).
5. The function only returns after `mutex` is successfully reacquired

## Semaphore

