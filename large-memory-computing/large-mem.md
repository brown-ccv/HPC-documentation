---
description: Memory-Intensive Workloads
---

# Large Memory Nodes on Oscar

Users can check the nodes in a partition using this command `nodes bigmem` . As of March 2020 the Oscar cluster currently has following nodes in bigmem partition.

```text
    NODES CORES  CPU/NODE    MEM     Features                  PARTITION
    2     64     2-cores     2096GB  32core,intel,cascade,edr  bigmem
    8     256    32-cores    376GB   32core,intel,cascade,edr  bigmem
    2     64     32-cores    754GB   32core,intel,cascade,edr  bigmem
```

To submit batch jobs to large memory nodes, include the following in your batch script:

```text
#SBATCH -p bigmem
```

To run an interactive job on large memory node, launch the `interact` command with the following flag:

```text
$ interact -q bigmem
```

