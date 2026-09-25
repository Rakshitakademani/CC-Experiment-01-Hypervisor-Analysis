# CC Experiment 01 – Hypervisor Performance Analysis

## About the Experiment

This Cloud Computing experiment compares the CPU performance of virtual machines running on two different hypervisor architectures:

- **Type-1 Hypervisor:** Proxmox VE
- **Type-2 Hypervisor:** VMware Workstation

The same CPU benchmark was executed inside Ubuntu virtual machines configured with the same basic resources.

## Objective

The objectives of this experiment are to:

1. Create an Ubuntu virtual machine using a Type-1 hypervisor.
2. Create an Ubuntu virtual machine using a Type-2 hypervisor.
3. Keep the virtual machine resources consistent for comparison.
4. Run the same Sysbench CPU benchmark on both systems.
5. Record execution time, total events, throughput, and latency.
6. Compare the observed benchmark results.

## Tools and Technologies

| Component | Details |
|---|---|
| Type-1 Hypervisor | Proxmox VE |
| Type-2 Hypervisor | VMware Workstation |
| Guest OS | Ubuntu 24.04 |
| CPU Allocation | 2 vCPU |
| Memory | 2 GB |
| Virtual Disk | 20 GB |
| Benchmark Tool | Sysbench 1.0.20 |
| CPU Benchmark | `sysbench cpu --cpu-max-prime=20000 run` |

## Experimental Setup

Both virtual machines were configured with:

- 2 virtual CPUs
- 2048 MB RAM
- 20 GB virtual disk
- Ubuntu guest operating system

The benchmark workload was kept the same on both virtual machines.

## Benchmark Procedure

Sysbench was installed in each Ubuntu VM using:

```bash
sudo apt update
sudo apt install sysbench -y
```

The installed version was checked using:

```bash
sysbench --version
```

The CPU benchmark was then executed using:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The experiment recorded the following values:

- Total execution time
- Total number of events
- Events per second
- Minimum latency
- Average latency
- Maximum latency
- 95th percentile latency

## Type-1 Hypervisor – Proxmox VE

The Proxmox VM was created with the required CPU, memory, disk, and network configuration. Ubuntu was installed and the system configuration was verified before running the benchmark.

The benchmark result recorded for the Proxmox VM was:

- **Total execution time:** 10.0005 s
- **Total events:** 17,494
- **Events per second:** 1,749.16
- **Minimum latency:** 0.57 ms
- **Average latency:** 0.57 ms
- **Maximum latency:** 2.43 ms
- **95th percentile latency:** 0.58 ms

## Type-2 Hypervisor – VMware Workstation

The VMware VM was configured with the same basic guest resources and Ubuntu was installed. The same system verification steps and Sysbench workload were used.

The benchmark result recorded for the VMware VM was:

- **Total execution time:** 10.0028 s
- **Total events:** 2,713
- **Events per second:** 271.14
- **Minimum latency:** 2.06 ms
- **Average latency:** 3.68 ms
- **Maximum latency:** 14.64 ms
- **95th percentile latency:** 5.37 ms

## Performance Comparison

| Metric | Proxmox VE (Type-1) | VMware Workstation (Type-2) |
|---|---:|---:|
| Total Execution Time | 10.0005 s | 10.0028 s |
| Total Events | 17,494 | 2,713 |
| Events per Second | 1,749.16 | 271.14 |
| Minimum Latency | 0.57 ms | 2.06 ms |
| Average Latency | 0.57 ms | 3.68 ms |
| Maximum Latency | 2.43 ms | 14.64 ms |
| 95th Percentile Latency | 0.58 ms | 5.37 ms |

### Observed Difference

For these recorded benchmark runs:

- Proxmox completed **14,781 more events** than VMware.
- Proxmox recorded **1,478.02 more events/sec**.
- The average latency recorded on Proxmox was **3.11 ms lower** than on VMware.
- The recorded maximum latency was **12.21 ms lower** on Proxmox.

These statements describe the results of these particular experimental runs; they should not be treated as a universal performance result for every hardware or software configuration.

## Screenshots

### Proxmox VE – Type-1

The Proxmox screenshots are stored in:

`screenshots/type1-proxmox/`

They document the VM creation, running state, Ubuntu console, system configuration, Sysbench output, and resource monitoring.

### VMware Workstation – Type-2

The VMware screenshots are stored in:

`screenshots/type2-vmware/`

They document the VM configuration, running state, system configuration, and Sysbench output.

### Comparison

The final comparison screenshot is stored in:

`screenshots/comparison/`

## Repository Structure

```text
CC-Experiment-01-Hypervisor-Analysis/
│
├── screenshots/
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.png
│   │   ├── 02-proxmox-vm-configuration.png
│   │   ├── 03-proxmox-vm-running.png
│   │   ├── 04-proxmox-ubuntu-console.png
│   │   ├── 05-proxmox-system-configuration.png
│   │   ├── 06-proxmox-sysbench-result.png
│   │   └── 07-proxmox-resource-monitoring.png
│   │
│   ├── type2-vmware/
│   │   ├── 01-vmware-vm-configuration.png
│   │   ├── 02-vmware-vm-running.png
│   │   ├── 03-vmware-system-configuration.png
│   │   └── 04-vmware-sysbench-result.png
│   │
│   └── comparison/
│       └── 01-hypervisor-performance-comparison.png
│
├── results/
│   └── performance-analysis.md
│
└── README.md
```

## How to Reproduce

1. Create an Ubuntu VM on Proxmox VE with the specified resources.
2. Create an Ubuntu VM on VMware Workstation with the same basic resources.
3. Install Sysbench in both VMs.
4. Run:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

5. Record the benchmark output.
6. Compare the recorded metrics.

## Conclusion

The experiment demonstrates how the two configured virtual environments performed under the same Sysbench CPU workload. The recorded runs produced different throughput and latency values, which are documented in the comparison table above.

All screenshots and benchmark observations for this experiment are included in this repository.
