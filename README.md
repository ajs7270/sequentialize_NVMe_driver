# NVMe Driver Sequentialization for HPC

This repository contains an experimental modification of the Linux NVMe driver aimed at increasing sequential I/O performance for high performance computing (HPC) workloads. The key change is in the `nvme_queue_rq` function, where requests are remapped to sequential sectors before being sent to the device.

Several kernel versions are provided to demonstrate compatibility and experimentation across releases:

- **4.9.1**
- **5.0.0**
- **5.1.15**

Precompiled modules are available in the `*.nvme.ko` directories. Source code for each version resides in its respective folder.

## Building

To build a module for your running kernel, change into the desired version directory and invoke `make`:

```bash
cd 5.1.15
make
```

The Makefile expects `KDIR` to point to the kernel build tree (defaults to `/lib/modules/$(uname -r)/build`). The resulting `nvme.ko` can then be inserted with `insmod` or `modprobe`.

Use the provided `clean` target to remove build artifacts:

```bash
make clean
```

## Benchmarking

Example FIO scripts (`fion1.sh`, `rfio.sh`, `sfio.sh`, etc.) are included for quick benchmarking. Adjust directory paths and job parameters to match your environment.

## Repository Structure

```
.
├── 4.9.1/          # Kernel 4.9.1 driver source
├── 5.0.0/          # Kernel 5.0.0 driver source
├── 5.1.15/         # Kernel 5.1.15 driver source
├── 4.9.1.nvme.ko/  # Prebuilt module for 4.9.1
├── 5.1.15.nvme.ko/ # Prebuilt module for 5.1.15
├── fion1.sh        # Sample FIO workload
└── ...
```

## Notes

- These changes are experimental and intended as a learning project. Use with caution in production environments.
- The code is derived from the Linux kernel and is therefore covered by the GPL-2.0 license.

## Portfolio Context

This project demonstrates low-level kernel development focused on I/O performance optimization. By modifying the NVMe request queueing logic and introducing sequential mapping, the driver can service workloads that benefit from reduced seek overhead. This repository is part of a portfolio showcasing interest and experience in systems programming, performance tuning, and Linux kernel internals.

