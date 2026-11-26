### Basics

primitive key value store with 4 ops - put(key,value), get(key), delete(key), scan(start, end)
when you create a python dict, its data lives in RAM.

CPU (executes instructions) -> CPU cache (very fast & small) -> RAM (fast, volatile memory) -> SSD/Disk (slower, persistent storage)

### Approx latency

CPU registers -
L1 cache
..
..
L4 cache
RAM
NVMe SSD random read (But survives a power loss)

Database engineering is about managing this performance difference

#### First problem: Persistence

suppose we execute ```balances["Alice"] = 500
Alice's balance is now $500. But what happens when we close the program?
the dict dissapears. When the program restarts, that data is gone unless we saved it somewhere.
