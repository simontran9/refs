# synchronization primitives

## Condition variables

### `pthread_cond_signal(pthread_cond_t *cond)`

Wakes up at least one of the threads that are currently blocked on the specified condition variable `cond`

### `pthread_cond_broadcast(pthread_cond_t *cond)`

Wakes up all threads currently blocked on the specified condition variable `cond`

### `pthread_cond_wait(pthread_cond_t *restrict cond, pthread_mutex_t *restrict mutex)`

1. Atomically releases mutual exclusion lock `mutex`
2. Block on condition variable `cond`
3. Wait for a signal from another thread on `cond`
4. When signaled/awakened by another thread, attempt to reacquire `mutex`. However, if another thread acquires `mutex`, then the signaled thread blocks, but this time, it's waiting for `mutex` (not for the `cond`).
5. The function only returns after `mutex` is successfully reacquired

