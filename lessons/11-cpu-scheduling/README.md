# CPU Scheduling: Choosing What Runs Next

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Explain why the OS scheduler exists.
- Compare common scheduling algorithms.
- Understand response time, waiting time, and throughput.

## 1. Why scheduling?
Many processes may be ready to run, but each CPU core can execute only a limited number of instruction streams at once. The **scheduler** chooses which ready task should run next.

## 2. Scheduling goals
- **CPU utilization:** keep the CPU usefully occupied.
- **Throughput:** completed jobs per unit time.
- **Turnaround time:** time from submission to completion.
- **Waiting time:** time spent waiting in the ready queue.
- **Response time:** time until the first response or first CPU service, depending on context.
These goals can conflict.

## 3. Algorithms
| Algorithm | Basic idea | Main drawback |
|---|---|---|
| First-Come, First-Served | Run in arrival order | Long jobs can delay short ones |
| Shortest Job First | Choose shortest expected CPU burst | Burst length is hard to know; long jobs may starve |
| Round Robin | Give each ready task a time quantum | Too-small quantum adds context-switch overhead |
| Priority | Prefer higher-priority tasks | Low-priority tasks may starve without controls |

## 4. Preemption and context switching
A **preemptive** scheduler can take the CPU away from a running task, for example when its time slice expires. A **context switch** saves one task's execution state and restores another's. Switching has overhead; it is not useful work for the application.

## 5. Practical thought experiment
Imagine three jobs arriving together with CPU bursts of 2, 4, and 8 time units. Compare FCFS with shortest-job-first on paper. Notice how the order changes average waiting time. This is a simplified model; real systems handle priorities, I/O, multicore CPUs, and dynamic behavior.

## Knowledge check
1. What does Round Robin allocate? **A time quantum to each ready task in turn.**
2. What is a context switch? **Saving/restoring execution state when changing the running task.**
3. Can scheduling goals conflict? **Yes; optimizing response time may not optimize throughput or fairness.**

## Key terms
Scheduler, ready queue, preemption, time quantum, context switch, throughput, turnaround time, starvation.

## Further reading
Study CPU scheduling chapters in an OS textbook and Linux scheduler documentation.
