# RTOS-and-other-embedded-topic
notes

## Table 
| Feature         | Cooperative Scheduling                                                       | Preemptive Scheduling                                                                       |
| --------------- | ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Control**     | The running process decides when to give up the CPU.                         | The scheduler can forcibly stop a running process.                                          |
| **Trigger**     | A task must reach a **yield point** or finish to allow the next task to run. | A higher-priority event or interrupt immediately stops the lower-priority task.             |
| **Typical Use** | Often used for tasks that take longer than **10 ms**.                        | Standard for **time-critical tasks**, typically shorter than **10 ms**.                     |
| **Risk**        | A single **greedy or hung task** can block the entire system.                | More complex to manage because the OS must save the **context (state)** of the paused task. |


### 1. Cooperative Scheduling

In this model, the scheduler is "polite." Even if a higher priority task becomes ready, it must wait for the current task to voluntarily release control.

    Process Flow: Process A runs → Process A finishes or yields → Scheduler picks Process B.

In AUTOSAR: This is commonly applied to background tasks that are not safety-critical and have execution times exceeding 10ms.

### 2. Preemptive Scheduling

This is the standard for real-time automotive systems. The scheduler is "authoritative" and prioritizes the most urgent task.

    Mechanism: If Task 1 (Low Priority) is running and an interrupt or a High Priority Task (e.g., a < 10ms safety check) arrives, the OS pauses Task 1 immediately.

Context Switching: The OS saves a "snapshot" of the paused task's registers and memory state so it can resume exactly where it left off later.

Hierarchy: Hardware interrupts (ISRs) from the Vector Table always preempt software tasks.


