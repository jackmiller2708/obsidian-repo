# Definition
A hash table is a data structure that uses a hashing function to store and retrieve data in a way that allows for efficient _insertion_, _deletion_, and _lookup_ of the data. In a hash table, a hash function is used to compute the index at which a given **key-value** pair should be stored in an array. The hash function takes the key as input and produces an integer index, which is then used to store the value at the corresponding array index. When a value is looked up, the hash function is used again to compute the index at which the key-value pair is stored, and the value is then returned.

Hash tables are commonly used in applications where *fast access to data is important*, because they offer constant-time complexity for the basic operations. This means that the time it takes to perform these operations is not dependent on the size of the data set, but is instead determined by the number of slots in the array used to store the data. This makes hash tables very efficient for large data sets.

Some people may refer to a hash table as an **[[Abstract Data Type (ADT)|ADT]]** because it provides a way to implement an ADT, even though a hash table is **not** an ADT itself. This can lead to confusion, since a hash table is a specific type of data structure, whereas an ADT is a mathematical model of a data type. It is generally more precise to refer to a hash table as a data structure and to an ADT as a mathematical model of a data type.

# Variations
There are several implementations of hash tables, including:

- **Hash map**: This is a specific implementation of a hash table that uses key-value pairs to store the data, it is the basic implementation of the hash table.
- **Chained hash table**: In this implementation, the separate chaining collision resolving is used.
- **Open-addressed hash table**: In this implementation, the [[Open-Addressing Collision Resolution|open-addressing collision resolving method]] is used.

There are trade-offs between these different implementations of hash tables. Chained hash tables can be more efficient in terms of memory usage, but they may be slower for lookup operations. Open-addressed hash tables can be faster for lookup operations, but they may require more memory and may be more susceptible to collisions.

# Collision Resolution
A [[Hash Collision|collision]] occurs when two or more keys are mapped to the same index in the array used to implement the hash table. This can cause problems if the hash table is not designed to handle collisions properly.

One way to resolve collisions is to use separate chaining, where each array index is used to store a linked list of values rather than a single value. When a key-value pair is added to the hash table, the hash function is used to compute the index at which the pair should be stored. If that index is already occupied, the value is added to the linked list at that index. When a value is looked up, the hash function is used again to compute the index at which the corresponding key-value pair is stored, and the value is then searched for in the linked list at that index.

Another way to resolve collisions is to use open addressing, where all of the data is stored in the array used to implement the hash table. When a key-value pair is added to the hash table, the hash function is used to compute the index at which the pair should be stored. If that index is already occupied, the algorithm will try the next index in the array until it finds an empty slot. When a value is looked up, the hash function is used again to compute the index at which the corresponding key-value pair is stored, and the value is then returned.

There are trade-offs between these different ways of resolving collisions. Separate chaining can be more efficient in terms of memory usage, but it may be slower for lookup operations. Open addressing can be faster for lookup operations, but it may require more memory.