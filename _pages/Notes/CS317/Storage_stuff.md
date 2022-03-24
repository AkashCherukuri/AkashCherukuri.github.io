- Cache Memory: cache-line-at-a-time (60-100ns)
- Flash Memory: Page-at-a-time (20-100 $\mu$s)
- Magnetic Disk: Page-at-a-time (5-10 ms)



## Magnetic Disks

Surface of the platter is divided into **tracks**, which are in turn divided into **sectors**. (A sector is ~512 Bytes)

Access Time - Seek Time (avg = 0.5worst, 0.333worst if all tracks have same number of sectors), Rotational Latency (avg = 0.5 worst), Data Transfer Rate

**Disk Block** - Unit for storage allocation and retrieval

- **Sequential Access Pattern** - Successive requests are for contiguous disk blocks, so seek only for the first block
- **Random Access Pattern** - Blocks can be anywhere, so need to seek for each block. This causes a lot of latency as time wasted for multiple seeks 



### Performance Measures

**IOPS** (I/O Per Second) is 50-200 for magnetic disks of the current generation.

**MTTF** (Mean Time to Failure) - The average time that the disk is expected to run continuously without failure; typically 3-5 years



### Flash Storage

*why is erasing shit tough* 

*how does remapping help with making it more efficient*

*parity blocks?????*

&nbsp;

&nbsp;

7 Hash functions and 10 bits apparently give the best performance, probabilistically speaking.
