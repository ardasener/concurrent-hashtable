## Concurrent hashtable

This is a concurrent hashtable implementation in C.

### Implementation

The hashtable uses the separate chaining technique as collision resolution strategy. This hashtable works by initially creating an empty array of `HASHSIZE` buckets. On first insertion to a bucket, a linked list structure is initialized. Each linked list structure contains a pointer to the head, the count of nodes, as well as a lock.

Each node structure contains a value and a next pointer. The nodes do not contain key/value pairs as it was built to store a spell-checking dictionary. However, this can be very easily implemented on each node.

The table supports `insert()`, `find()`, and `remove()` methods currently. 

(Note: This is a very naive approach with a constant size hashtable. No load-balancing was implemented.) 

### Usage

Passing in dictionaries (provided in `dictionaries/`) as command line arguments will spawn a new thread for each dictionary.

Passing in the option `-p` before dictionaries will plot the hash distribution. This requires `gnuplot` to be installed first.

First clone and run `make`.

Then:
```
./table dictionaries/francias.txt dictionaries/espanol.txt <more dictionaries...>

./table -p <dictionaries...>
```

#### Example distribution plot
![Distribution Plot](distribution_plot.png)

The `x-axis` indicates hashtable buckets, the `y-axis` indicates the number of linked list nodes.

### Notes on concurrency

The hashtable is not lock-free. Additionally, the locks are implemented per linked list (bucket). This allows for manipulation of other buckets without having to lock the entire hashtable.
