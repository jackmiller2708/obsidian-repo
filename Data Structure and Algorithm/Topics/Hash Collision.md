Tags: #data-structure #hash-collision

A hash collision or clash is when two pieces of data in a [[Hash Table|hash table]] share the same hash value. The hash value in this case is derived from a hash function which takes a data input and returns a fixed length of bits.

Hash collisions can be unavoidable depending on the number of objects in a set and whether or not the bit string they are mapped to is long enough in length. When there is a set of _n_ objects, if _n_ is greater than |_R_|, which in this case _R_ is the range of the hash value, the probability that there will be a hash collision is 1, meaning it is guaranteed to occur.

Hash collisions can occur by chance and can be intentionally created for many hash algorithms. The probability of a hash collision thus depends on the size of the algorithm, the distribution of hash values, and whether or not it is both mathematically known and computationally feasible to create specific collisions.