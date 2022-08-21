# Storage Structures

Disks are usually connected to the system using SATA (serial ATA), SAS (serial attached SCSI) or NVMe (Non Volatile Memory access). Storage networks are of two types: SAN (storage area networks) or NAS (network attached storage)

- Cache Memory: cache-line-at-a-time (60-100ns)
- Flash Memory: Page-at-a-time (20-100 $\mu$s)
- Magnetic Disk: Page-at-a-time (5-10 ms)



## Magnetic Disks

Surface of the platter is divided into **tracks**, which are in turn divided into **sectors**. (A sector is ~512 Bytes)

Access Time (time between request issuance and data transfer starting) = Seek Time (avg = 0.5worst, 0.333worst if all tracks have same number of sectors) + Rotational Latency (avg = 0.5 worst), Data Transfer Rate

**Disk Block** - Unit for storage allocation and retrieval

- **Sequential Access Pattern** - Successive requests are for contiguous disk blocks, so seek only for the first block
- **Random Access Pattern** - Blocks can be anywhere, so need to seek for each block. This causes a lot of latency as time wasted for multiple seeks 



### Performance Measures

**IOPS** (I/O Per Second) is 50-200 for magnetic disks of the current generation.

**MTTF** (Mean Time to Failure) - The average time that the disk is expected to run continuously without failure; typically 3-5 years

**Annualized Failure Rate** (AFR) = (365\*24/MTTF)\*100%



## Flash Storage

NAND flash is cheaper than NOR Flash and doesn’t have a big difference between sequential and random read. However, pages can be written ONLY ONCE, and must be erased to allow rewriting them.

Erase happens in units of **erase blocks** where in the logical page address is remapped to a different free physical page address. Note that en erase block is much larger than a logical page. This remapping is tracked by the **Flash Translation Table**, and this is carried out by the **Flash Translation Layer**.

Note that after $\sim 10^5$ erases, the erase block becomes unreliable and cannot be used. (Never fill up an SSD to nearly full)

SSDs alaso support parallel reads.

&nbsp;

# Raid: Redundant Arrays of Independent Disks

We wish to have **high capacity, high speed and high reliability**. We store the data redundantly so that the extra information can be used to rebuild information lost on disk failure.

#### Block-Level Striping

Given $n$ disks, the $i^{th}$ block of a file goes to the disk $(i\text{ mod }n)+1$.

### RAID Level 0

Block Level Striping is used, there is no redundancy. Used when data-loss is not critical.

### RAID Level 1

Mirrored disks with block level striping. That is, we have $2n$ disks where the $i^{th}$ and $(n+i)^{th}$ disks are completely identical.

### RAID Level 5

A **parity block** $j$ stores the XOR of the bits from block $j$ of each disk. Raid Level 5 has a disk dedicated for storing the parity blocks for all blocks. XOR of the remaining blocks can be computed to attain the corrupted/lost block in a s.

### RAID Level 6

$(P+Q)$ redundancy is present where two error correction blocks are used instead of a single parity block to guard against multiple disk failures.

Note that any one disk can be read upon random, as they are completely identical.

**Software RAID** has the implementation done entirely in software with no special hardware support. **Hardware RAID** on the other hand has special hardware. New hardware errors are possible here, like power failure resulting in corrupted disk. A full scan of disk might be required when this occurs. Or we could write into NV-RAM and then copy over from there.

Some other hardware failures are:

- **Latent Sector Failure** - data written successfully earlier gets damaged. **Data Scrubbing** means to continually scan for Latent Sector failures, and recover loss from the parity/copy disks.

  **Hot Swapping** allows the replacement of a disk when the system is still running. Spare disks are usually kept online and are switched to when a failure is detected.

  

## Disk Block Access Optimization

1. **Buffer** the results to be used later in memory
2. **Read-ahead** extra blocks from a track assuming they’ll be asked for soon
3. **Disk Arm Scheduling** refers to scheduling the requests to have less arm movement. (The **elevator algorithm** is used)