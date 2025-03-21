# concurrency patterns

## Producer-consumer/bounded-buffer problem

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
