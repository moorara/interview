# Unix/Linux

## KVM

  - Kernel-based Virtual Machine
  - A virtualization infrastructure for Linux Kernel which turns it into a hypervisor.
  - Requires a processor with hardware virtualization capability (Intel VT-x or AMD-V).

### Hypervisor

  - **Type-1: Native Hypervisors**
    - These hypervisors run directly on the host's hardware
  - **Type-2: Hosted Hypervisors**
    - These hypervisors run on a conventional OS as a computer program.
    - A guest operating system runs as a process on the host.


## File Permissions

  - File Type:
    - Directory (d)
    - Symbolic Link (l)
  - Permission Groups:
    - Owner (u)
    - Group (g)
    - All Users (a)
  - Permission Types:
    - Read (r = 4)
    - Write (w = 2)
    - Execution (x = 1)
  - Advanced Permissions:
    - Setuid/Setgid (s)
    - Sticky Bit (t)


## Linux Control Groups

  - **cgroups** is a Linux kernel feature that limits, profiles, and isolates the resource usage of a collection of processes.
  - Each subsystem (system resource) has its own independent hierarchy (tree) of groups
  - System Resources (Subsystems):
    - CPU (cpu, cpuset, cpuacct)
    - Memory (memory)
    - I/O (blkio)
    - Devices (devices)
    - Network (net_cls, net_prio)
    - Namespace (ns)
    - Freezer (freezer)
  - cgroups provide:
    - Limiting
    - Prioritization
    - Controlling
    - Acounting


## Linux Namespaces

  - **Namespaces** provide processes with their own system view.
  - Each process is in one namespace of each type.
  - Namespaces:
    - PID (pid)
    - Network (net)
    - Mount (mnt)
    - UTS (uts)
    - IPC (ipc)
    - User (user)


## Linux Containers

  - Containers leverage Linux **cgroups + namespaces** to run multiple isolated groups of processes.
  - cgroups functionality allows limitation and prioritization of resources (cpu, memory, I/O, network, ...).
  - namespace functionality allows complete isolation of an application’s view of the os (process tree, file system, network interface, ...).

  - Container vs. VM:
    - Containers are not lightweight virtual machines!
    - Virtual machines and containers are both solutions to software isolation.
    - Virtual machines provide full isolation, require more resources, and take minutes to start.
    - Containers give less isolation, require much less resources, and take milliseconds to start.

