# FreeRTOS Real-Time Operating System Notes

[中文](README.md) | [English](README-English.md)

This repository organizes learning materials about the FreeRTOS real-time operating system. It covers RTOS fundamentals, task scheduling, kernel objects, inter-task communication, interrupt management, low-power operation, and memory management. The content is based on the PDF and DOCX materials in `docs/` and is suitable for FreeRTOS study on STM32 and other embedded platforms.

## Materials

- [FreeRTOS Real-Time Operating System PDF](docs/FreeRTOS实时操作系统.pdf)
- [FreeRTOS Real-Time Operating System DOCX Source](docs/FreeRTOS实时操作系统.docx)

## Learning Roadmap

```text
RTOS fundamentals
    ├── Bare-metal programming and RTOS
    ├── FreeRTOS features
    ├── Task scheduling
    └── Task states
            ↓
Porting and task management
    ├── Source structure and system configuration
    ├── FreeRTOS porting
    ├── Task creation and deletion
    ├── Task suspension and resumption
    └── Time-slice scheduling
            ↓
Real-time services
    ├── Interrupt management
    ├── Time management
    ├── Message queues
    ├── Semaphores and mutexes
    ├── Queue sets, event groups, and task notifications
    └── Software timers
            ↓
System-level optimization
    ├── Tickless low power
    └── FreeRTOS memory management
```

## Contents

### Chapter 1: RTOS Introduction

- Compare bare-metal programming and RTOS-based development in task scheduling, hardware management, and complexity.
- Understand the open-source, lightweight, and portable characteristics of FreeRTOS.
- Build a basic model of tasks, schedulers, and real-time systems.

### Chapter 2: FreeRTOS Fundamentals

- Understand the basic operation of the task scheduler.
- Learn the running, ready, blocked, and suspended task states.
- Understand how priority and state changes affect scheduling.

### Chapter 3: FreeRTOS Porting

- Learn how to obtain the FreeRTOS source code and understand its directory structure.
- Add the kernel source code to an embedded project.
- Configure `FreeRTOSConfig.h` and other system configuration files.
- Modify `stm32f1xx_it.c` to adapt FreeRTOS to an STM32 project.
- Understand the relationship between the tick interrupt, memory configuration, and system interrupts.

### Chapter 4: Task Creation and Deletion

- Learn the APIs for dynamic task creation, static task creation, and task deletion.
- Understand task functions, task stacks, task control blocks, and task priorities.
- Compare dynamic and static allocation.
- Verify task execution with dynamic and static task-creation experiments.

### Chapter 5: Task Suspension and Resumption

- Suspend and resume tasks with the relevant APIs.
- Understand task resumption in normal task context and interrupt context.
- Observe task-state transitions through experiments.

### Chapter 6: FreeRTOS Interrupt Management

- Learn the principles of interrupt management in FreeRTOS.
- Understand interrupt enable/disable operations, critical sections, and scheduler suspension.
- Distinguish APIs that can be called from interrupts from normal task APIs.
- Use a timer-interrupt experiment to understand cooperation between interrupts and task scheduling.

### Chapter 7: Time-Slice Scheduling

- Understand round-robin scheduling among tasks with the same priority.
- Observe execution order under time-slice scheduling.
- Analyze the relationship between task priority, time slices, and system ticks.

### Chapter 8: Task APIs

- Query task state and task information.
- Obtain task runtime statistics and system task statistics.
- Analyze system behavior through task-state and runtime-statistics experiments.

### Chapter 9: Time Management

- Understand FreeRTOS delay functions and blocking delays.
- Yield the CPU with task delays and observe scheduling behavior.
- Connect the system tick with task wake-up timing.

### Chapter 10: Message Queues

- Understand queues as a mechanism for transferring data between tasks.
- Learn queue creation, message sending, and message receiving.
- Transfer data between tasks and between interrupts and tasks.
- Verify producer-consumer communication with queue experiments.

### Chapter 11: Semaphores

- Understand binary and counting semaphores.
- Use semaphores for synchronization and resource counting.
- Understand priority inversion and its impact.
- Protect shared resources with mutexes and reduce priority-inversion risk through priority inheritance.

### Chapter 12: Queue Sets

- Understand the purpose and use cases of queue sets.
- Wait for events from multiple queues or semaphores through one queue set.
- Manage multiple communication objects in a unified way.

### Chapter 13: Event Groups

- Understand event groups and event bits.
- Represent and combine multiple system conditions with event bits.
- Compare event groups with semaphores.
- Implement multi-condition waiting and synchronization.

### Chapter 14: Task Notifications

- Understand task notifications as a lightweight communication mechanism.
- Use task notifications to simulate binary semaphores, message mailboxes, and event groups.
- Understand their efficiency when communication is directed to a specific task.

### Chapter 15: Software Timers

- Understand software timers and their states.
- Distinguish one-shot timers from periodic timers.
- Learn software-timer APIs and callback functions.
- Implement periodic operations with software timers.

### Chapter 16: Tickless Low-Power Mode

- Understand the goal of RTOS low-power operation.
- Learn how Tickless mode reduces unnecessary system ticks.
- Configure the main Tickless options.
- Observe idle-time low-power behavior through an experiment.

### Chapter 17: FreeRTOS Memory Management

- Understand the basic mechanism of dynamic memory allocation in FreeRTOS.
- Learn the characteristics of `heap_1`, `heap_2`, `heap_3`, `heap_4`, and `heap_5`.
- Select a memory algorithm according to deallocation support, fragmentation, multiple memory regions, and system requirements.
- Learn the FreeRTOS memory-management APIs.
- Observe dynamic allocation and deallocation through an experiment.

## Core Concepts

| Concept | Role |
| --- | --- |
| Task | The basic program unit scheduled for execution |
| Scheduler | Selects a task according to state and priority |
| Priority | Determines the relative scheduling importance of a task |
| Ready state | The task can run and is waiting for scheduling |
| Blocked state | The task is waiting for time, a queue, a semaphore, or another event |
| Suspended state | The task is explicitly suspended and excluded from normal scheduling |
| Queue | Transfers data between tasks or between an interrupt and a task |
| Binary semaphore | Synchronizes events or coordinates simple resources |
| Counting semaphore | Counts resources or accumulated events |
| Mutex | Protects shared resources and supports priority inheritance |
| Event group | Represents and waits for combinations of event bits |
| Task notification | A lightweight notification mechanism directed to a task |
| Software timer | A timer managed by the timer service task |
| Tickless | Reduces system ticks during idle periods to lower power consumption |
| Heap scheme | A FreeRTOS dynamic-memory management algorithm |

## Communication Mechanisms

| Mechanism | Main use | Typical characteristic |
| --- | --- | --- |
| Message queue | Transfer structured data or messages | Supports multiple messages and producer-consumer designs |
| Binary semaphore | Event synchronization | Has available and unavailable states |
| Counting semaphore | Resource or event counting | Represents multiple resources or accumulated events |
| Mutex | Protect shared resources | Supports priority inheritance |
| Queue set | Wait for multiple communication objects | Unifies multiple queues or semaphores |
| Event group | Wait for multiple conditions | Combines system states with event bits |
| Task notification | Direct notification to one task | Low overhead and fast for targeted communication |

## Dynamic and Static Creation

| Method | Characteristic | Suitable scenario |
| --- | --- | --- |
| Dynamic creation | Allocates the task control block and stack from the FreeRTOS heap | Flexible task count or lifetime |
| Static creation | The application provides the task control block and stack | Deterministic memory use and no runtime allocation |

The choice should consider memory policy, task lifetime, real-time requirements, and fault-recovery needs.

## Suggested Study Process

1. Learn task states, priorities, and the scheduler before studying communication mechanisms.
2. Complete the dynamic task experiments first, then compare them with static allocation.
3. For every API, record its calling context, blocking behavior, timeout parameters, and interrupt safety.
4. Master queues, binary semaphores, and mutexes before studying queue sets, event groups, and task notifications.
5. Use task-state queries and runtime statistics to locate scheduling, blocking, and priority problems.
6. Analyze low power and memory management together with the MCU RAM, system tick, and task lifetimes.

## Directory Structure

```text
freertos-learning-notes/
├── README.md
├── README-English.md
└── docs/
    ├── FreeRTOS实时操作系统.pdf
    └── FreeRTOS实时操作系统.docx
```

## Current Scope

The repository currently focuses on the FreeRTOS course PDF, DOCX source, and learning index. It does not include additional FreeRTOS source code, porting projects, or experiment code. Future work can add STM32 projects, `FreeRTOSConfig.h`, task-communication examples, performance records, and low-power test results by chapter.

## Keywords

`FreeRTOS` `RTOS` `Task Scheduling` `Queue` `Semaphore` `Mutex` `Event Group` `Task Notification` `Software Timer` `Tickless` `Memory Management` `Embedded Systems`
