# Memory and cache optimizations

## Memory hierarchy

## Custom memory allocators

## Cache optimization

### Cache line

A cache line is a fixed-size block of data, typically 64 bytes, that is transferred between the CPU cache and main memory. Particularly, it is the smallest unit of data that can be fetched from memory — the CPU cannot retrieve only a few bytes or words.

When a cache line is copied from memory into the cache, it forms a cache entry, which includes the copied data and the corresponding memory location, called a tag.

Whenever the CPU needs data that's already in the cache (i.e. if the cache line containing that data is present), it's a cache hit, and the data can be accessed quickly, but if the data is not in the cache, it's a cache miss, and the CPU needs to fetch the entire cache line from main memory, which is a slower operation. Therefore, accessing other values from the same cache line is cheap, and so we usually want to align our data such that it minimizes the amount of different cache lines it touches! Also, it's why CPUs will often prefetch, which is the process of fetching data or instructions from main memory into the cache before they are actually needed.
