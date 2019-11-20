# Operating Systems

**Process Hierarchies**

  - Process Session
    - Process Group
      - Process


**Inter-Process Communications**

  - Signal
  - Shared Memory
  - Message Passing
  - Memory-Mapped File


**Synchronization Mechanisms**

  - Atomic Instructions:
    - test-and-set
    - fetch-and-add
    - compare-and-swap


  - Mutual Exclusions:
    - Spin lock
    - Lock (Mutex)
    - Semaphore
    - Read-Write Lock
    - Condition Variable
    - Monitor
    - Barrier
    - Message-Passing


**Computer Architecture**

  - Cache
    - Locality:
      - Spatial Locality
      - Temporal Locality


  - Memory:
    - SRAM: static, 6 transistors per bit, fast, less power, more expensive
    - DRAM: dynamic, 1 transistor + 1 capacitor per bit, slow, requires refreshing


  - Storage Hierarchies:
    - Registers  -->  Cache  -->  RAM  -->  SSD  -->  HDD


  - Parallelism:
    - Instruction-Level:
      - Scalar Pipelining
      - Superscalar Pipelining
      - Out-of-Order Execution (Dynamic Scheduling)
    - Thread-Level:
      - Coarse-Grain Multithreading
      - Fine-Grain Multithreading
    - Process-Level:
      - Multicore --> Synchronization, Cache Coherency, Memory Consistency

