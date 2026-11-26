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

suppose we execute `balances["Alice"] = 500`
Alice's balance is now $500. But what happens when we close the program?
the dict dissapears. When the program restarts, that data is gone unless we saved it somewhere.

That is because RAM is volatile memory. The database needs persistence: the ability to retain data after the process terminates
or the computer restarts. (Write ahead logging)

#### Why not store everything on disk?

we could write every update directly to disk

```
with open("database.txt", "w") as file:
    file.write("Alice,500")
```

Now the data can survive a program restart. but imagine we have a million customers and thousands of transactions per second. Constantly accessing and rewriting files becomes ineffecient.

We have a trade-off between RAM-based database (fast reads and writes but data lost on power failure) and Disk-based database (persistent data, larger storage capacity but slower access)
Modern databases do both. They keep frequently accessed data in memory, organize persistent data on disk, and implement mechanisms to recover after failures.
