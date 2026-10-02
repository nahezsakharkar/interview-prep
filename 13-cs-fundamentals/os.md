---
title: "Operating Systems"
tags: ["cs-fundamentals","os"]
difficulty: medium
status: revised
last_reviewed: 2026-10-02
---

# Operating Systems

## Definition

An Operating System (OS) is the system software that manages computer hardware and software resources and provides common services for computer programs. It acts as an intermediary between the user and the computer hardware.

## Core Concepts

### 1. Processes vs. Threads
A **Process** is an independent program in execution with its own memory space (Stack, Heap, Data). A **Thread** is the smallest unit of execution within a process; multiple threads within a process share the same memory space.

| Feature | Process | Thread |
| :--- | :--- | :--- |
| **Memory** | Independent space | Shared space |
| **Creation** | Heavyweight (expensive) | Lightweight (cheap) |
| **Communication** | IPC (Sockets, Pipes, Shared Mem) | Shared variables (risky) |
| **Isolation** | High (crash doesn't affect others) | Low (crash can kill process) |

### 2. CPU Scheduling
The OS uses a scheduler to decide which process gets the CPU.
- **First-Come, First-Served (FCFS)**: Simple, but suffers from the "convoy effect" (short tasks wait for long ones).
- **Shortest Job First (SJF)**: Optimal for average wait time, but requires knowing job length in advance.
- **Round Robin (RR)**: Each process gets a fixed time slice (quantum). Fair and prevents starvation.
- **Priority Scheduling**: High-priority tasks run first. Risk: **Starvation** (low-priority tasks never run). Mitigation: **Aging** (gradually increase priority over time).

### 3. Concurrency and Synchronization
When multiple threads access shared data, **Race Conditions** occur.
- **Mutex (Mutual Exclusion)**: A lock that ensures only one thread enters a critical section.
- **Semaphore**: A counter that controls access to a finite number of resources.
- **Deadlock**: A situation where Process A holds Resource 1 and waits for Resource 2, while Process B holds Resource 2 and waits for Resource 1.

**The Four Necessary Conditions for Deadlock**:
1. **Mutual Exclusion**: Only one process can use a resource at a time.
2. **Hold and Wait**: A process holds a resource while waiting for another.
3. **No Preemption**: Resources cannot be forcibly taken away.
4. **Circular Wait**: A closed chain of processes waiting for each other.

## Memory Management

### Virtual Memory and Paging
To allow programs larger than physical RAM to run, the OS uses **Virtual Memory**.
- **Paging**: Memory is divided into fixed-size blocks called "pages".
- **Page Table**: Maps virtual addresses to physical frames in RAM.
- **Page Fault**: Occurs when a program accesses a page not currently in RAM. The OS must fetch it from disk.
- **Thrashing**: A state where the system spends more time swapping pages in and out of disk than executing instructions.

## Working Code Example: Deadlock Simulation (Java)

This example demonstrates a classic circular wait deadlock.

```java
public class DeadlockDemo {
    public static Object Lock1 = new Object();
    public static Object Lock2 = new Object();

    public static void main(String[] args) {
        // Thread 1: Lock1 -> Lock2
        new Thread(() -> {
            synchronized (Lock1) {
                System.out.println("T1: Locked Lock1");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (Lock2) {
                    System.out.println("T1: Locked Lock2");
                }
            }
        }).start();

        // Thread 2: Lock2 -> Lock1
        new Thread(() -> {
            synchronized (Lock2) {
                System.out.println("T2: Locked Lock2");
                try { Thread.sleep(100); } catch (Exception e) {}
                synchronized (Lock1) {
                    System.out.println("T2: Locked Lock1");
                }
            }
        }).start();
    }
}
```
**Complexity**: Time $O(1)$; Space $O(1)$. The result is a permanent hang.

## Interview questions

### Q1: What is a Context Switch?
**Model answer**: A context switch is the process of storing the state (registers, program counter) of a running process/thread so it can be paused and another resumed. This is expensive because it involves saving state to the PCB (Process Control Block) and potentially flushing CPU caches.

### Q2: Difference between a Mutex and a Semaphore?
**Model answer**: A Mutex is a binary lock used for mutual exclusion—only the thread that locked it can unlock it. A Semaphore is a counter used for signaling; any thread can increment (signal) or decrement (wait) the counter.

### Q3: How does the OS prevent Deadlocks?
**Model answer**: 
1. **Prevention**: Eliminate one of the four conditions (e.g., force processes to request all resources at once).
2. **Avoidance**: Use algorithms like the **Banker's Algorithm** to check if granting a resource leads to an unsafe state.
3. **Detection & Recovery**: Allow deadlock to happen, detect it via a Wait-For Graph, and kill/restart a process to break the cycle.

### Q4: What is a Page Fault and how is it handled?
**Model answer**: A page fault happens when the CPU tries to access a virtual address not currently in physical RAM. The OS: 1) Traps the error, 2) Finds the page on disk, 3) Finds a free frame in RAM (swapping out another page if necessary), 4) Loads the page, and 5) Restarts the instruction.

### Q5: What is the "Critical Section Problem"?
**Model answer**: It is the challenge of designing a protocol where only one process can execute a piece of code that accesses shared resources at a time. A solution must satisfy: Mutual Exclusion, Progress (no indefinite blocking), and Bounded Waiting.

## Related notes

- [Networking](networking.md)
- [OOP and Design Basics](oop.md)
- [JVM Internals](../02-languages/java/jvm-internals.md)
