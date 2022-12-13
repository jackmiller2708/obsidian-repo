Tags: #collision #open-addressing

**Open addressing** is a method of resolving [[Hash Collision|collisions]] in a [[Hash Table|hash table]].

In the open-addressing method, all of the data is stored in the array used to implement the hash table. When a key-value pair is added to the hash table, the hash function is used to compute the index at which the pair should be stored. If that index is already occupied, the algorithm will try the next index in the array until it finds an empty slot. When a value is looked up, the hash function is used again to compute the index at which the corresponding key-value pair is stored, and the value is then returned.

The steps for resolving collisions using the open-addressing method in a hash table are as follows:

1. A key-value pair is added to the hash table.
2. The hash function is used to compute the index at which the pair should be stored in the array.
3. If the index is already occupied, the algorithm will try the next index in the array until it finds an empty slot.
4. The key-value pair is stored at the empty slot found in step 3.
5. When a value is looked up, the hash function is used again to compute the index at which the corresponding key-value pair is stored.
6. The value is then returned from the array at the index computed in step 5.

Below is an exemplary implementation of a hash table with the open-addressing collision resolution method:

```TypeScript
class HashTable {
  private size: number;
  private table: any[];
  
  constructor(size: number) {
    this.size = size;
    this.table = new Array(this.size);
  }
  
  private hash(key: number): number {
    return key % this.size;
  }

  public insert(key: number, value: any): void {
    let idx = this.hash(key);
    
    if (this.table[idx] === undefined) {
      this.table[idx] = value;
      this.size += 1;
    }

    // implement open addressing
    let i = 0;

    while (this.table[idx] !== undefined) {
      i += 1;
      idx = (idx + i ** 2) % this.size;
    }

    this.table[idx] = value;
    this.size += 1;
  }

  public search(key: number): number {
    let idx = this.hash(key);

    if (this.table[idx] === undefined) {
      return undefined;
    }

    let i = 0;
    
    while (this.table[idx] !== undefined) {
      if (this.table[idx] === key) {
        return idx;
      }

      i += 1;
      idx = (idx + i ** 2) % this.size;
    }
    
    return undefined;
  }
}
```

Open addressing is a way of resolving collisions in a hash table by using the array itself to store the data. This can be more efficient in terms of memory usage than other collision resolution techniques, such as separate chaining, where each array index is used to store a linked list of values. However, open addressing can be more susceptible to collisions and may be slower for lookup operations.