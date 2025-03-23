# Classic concurrency problems

## Producer-consumer/bounded-buffer problem

### Description

TO DO

### Anatomy

- The conditional variable is used to notify the consumer that there are items in the buffer to process
- The predicate expression is necessary to "save" the signal, Otherwise, if all consumer threads are busy processing when the producer adds a new item and signals, the signal will be missed and forgotten, and when the consumer threads are done their work, they will be incorrectly waiting, despite their being more items to process.
- The mutual exclusion lock is used to prevent data races on the shared data (in this case, the buffer, and the predication expression variable). For example, in a scenario with a single producer and a single consumer, the consumer thread might check the predicate expression to see that there are no items in the buffer. Then, the scheduler may perform a a context switch, which switches the running task to the producer, that'll modify the predication expression and signal, followed by another context switch back to the consumer thread, which misses the signal, and proceeds with the call to `pthread_cond_wait()` when the producer had produced an item.
- The while loop is necessary with the predicate_expression as the condition (over a simple if statement) because it's possible that when the consumer thread unblocks on the condition variable, and attempts to re-acquire the mutual exclusion lock, a different consumer thread may instead acquire it and consume (i.e. dequeue an item from the buffer and process it), therefore modifying the the predicate_expression. Hence, the predicate_expression must be checked again, and the consumer thread that did not manage to re-acquire the mutex lock must wait again. Otherwise, it would proceed when it shouldn't. 

```c
#include <pthread.h>
#include <stdbool.h>

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond_var = PTHREAD_COND_INITIALIZER;

producer() {
    pthread_mutex_lock(&mutex);
    // Change shared state
    predicate_expression = true;
    pthread_cond_signal(&cond);
    pthread_mutex_unlock(&mutex);
}

consumer() {
    pthread_mutex_lock(&mutex);
    while (!predicate_expression) {
        pthread_cond_wait(&cond, &mutex);
    }
    // The predicate is now true, do work
    // ...
    pthread_mutex_unlock(&mutex);
}
```

## Dining philosopher's problem
