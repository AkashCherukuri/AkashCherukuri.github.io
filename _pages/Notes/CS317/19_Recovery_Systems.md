---
title: Recovery Systems
permalink: /notes/cs317/rec_sys
classes: wide
author_profile: false
# sidebar:
#     nav: "notes_cs337"

---

<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>

<!-- Notes Begin from here -->



Failures are classified into three types:

1. **Transaction Failures** - Can be due to erroneous logic in queries or system errors causing deadlocks
2. **System Crashes**
3. **Disk Failures**

There are two main kinds of blocks:

- **Physical Blocks** are the blocks residing on the disk
- **Buffer Blocks** are temporary blocks in main memory

`input(B)` transfers a physical block to the main memory, whereas `output(B)` transfers a block from the **buffer** to the disk. We assume each data item to fit in a single physical block.

Each transaction $T_i$ has its own copy of a data item $X$ called $X_i$. `read(X)` by the transaction assigns $X$ to $X_i$ and `write(X)` by the transaction would send $X_i$ to the buffer. The system can call `output(B)` to transfer this buffer block to main memory when it deems fit.



## Log Based Recovery

Log is a sequence of log records which store information about the activities made by a transaction in a database. Consider the transaction $T_i$.

| Activity                     | Log                              |
| ---------------------------- | -------------------------------- |
| Transaction start            | $<T_i, \text{start}>$            |
| `write(X)` executed          | $<T_i, X,V_{before}, V_{after}>$ |
| Last statement of $T_i$ done | $<T_i, \text{commit}>$           |

**Immediate Modification** scheme lets the updates of a transaction to be sent to the buffer / disk before the transaction commits. **Note that log record must be written before execution of query!** On the other hand, **Deferred-modification** scheme performs the updates to disk only at the time of commit.

> If $T_i$ modifies an item $X$, no other transaction is allowed to modify $X$ until $T_i$ either commits or aborts

`undo(T_i)` restores original values of data items that were updated by $T_i$. For every write $<T_i, X, V_1, V_2>$ we add a special log record $<T_i, X, V_1>$. $<T_i, \text{abort}>$ is written out once the abort it completed.

`redo(T_i)` on the other hand simply executes all the records sequentially.



## Checkpoints

Periodically save the state of the database to streamline recovery procedure.

- Output all log records currently in memory to stable memory
- Output all modified buffer blocks to disk
- Write a record $<\text{checkpoint}, L>$ onto the stable memory where $L$ is a list of all active transactions at that time
- **All updates are stopped while checkpointing!** (Fuzzy checkpoints try to fix this)



## Recovery Algorithm

There are two main phases to the recovery algorithm; redo and undo phases.

### Redo Phase

1. Find the last checkpoint $<\text{checkpoint},L>$ and set `undo_list` to be $L$
2. Scan forward and redo all write operations. Add $T_i$ to `undo_list` when $<T_i, \text{start}>$ is found and remove $T_i$ from `undo_list` when either $<T_i, \text{commit}>$ or $<T_i, \text{abort}>$ are found.

### Undo Phase

1. Scan the log backwards from the end
2. Undo write operations $<T_i,X,V_1,V_2>$ by adding $<T_i, X, V_1>$ where $T_i$ belongs to `undo_list`
3. Remove $T_i$ from `undo_list` and add log line $<T_i, \text{abort}>$ upon encountering $<T_i, \text{start}>$
4. Stop when `undo_list` is empty



## Buffering

Log records are generally buffered by storing them in memory instead of sending them to stable memory to improve I/O. They are flushed when a block is either full or `log_force` is called. `log_force` is usually called when a transaction commits. 

**Write-Ahead-Logging (WAL)**: Before a block of data in main memory is output to database, the corresponding log block must be flushed to the stable memory

Database also has a buffer, which has three behaviors based on how the blocks are pushed to database. **No-force policy** is when the updated blocks need not be pushed when a transaction commits, **force policy** is when the blocks are pushed when a transaction commits (not before) and **steal policy** is when blocks can be pushed even before a transaction commits. 

1. Acquire a latch on the block
2. Flush logs
3. Output block to disk
4. Release latch on the block



## Fuzzy Checkpoints

All updates have to be stopped during checkpointing, which is inefficient. Fuzzy checkpointing aims to solve this issue.

1. Temporarily stop updates
2. Write $<\text{checkpoint},L>$ and force logs to stable storage
3. Note the list $M$ of modified blocks
4. Allow transactions’ actions to resume 
5. Output all blocks in $M$ to disk following WAL
6. Store a pointer to checkpoint in a fixed memory on disk called `last_checkpoint`



## Remote Backup Systems

“Heartbeat” messages are sent between the primary and the backup sites so they know the other’s status. To transfer control to the backup, use its copy of the database and the logs generated by the primary to recover data. The transactions that were incomplete are rolled back.

To reduce recovery time, the backup periodically processes redo logs so its database is kept up-to-date with the primary site. **Hot-spare** configuration lets the backup continually process log files as they come in.

Durability is of three levels;

- **One-safe**: Commit as soon has transaction’s commit log is written in primary
- **Two-very-safe**: Commit when transaction’s log is written in both primary and backup
- **Two-safe**: Proceed as two-very-safe when both are up, and as one-safe if only primary is active
