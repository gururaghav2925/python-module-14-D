#  Round Robin Scheduling Algorithm in Python

## Aim
To calculate:- Completion Time, Turn Around Time (TAT), Waiting Time (WT)
for multiple processes using **Round Robin Scheduling**, where all arrival times are 0.

---

## 📌 Definitions

- **Completion Time (CT):** Time at which a process finishes execution.
- **Turn Around Time (TAT):** Time taken from arrival to completion.  
  `TAT = Completion Time - Arrival Time`
- **Waiting Time (WT):** Time spent waiting in the ready queue.  
  `WT = Turn Around Time - Burst Time`

---

## 🔄 Round Robin Logic

- Each process gets executed for a fixed time quantum.
- If a process's remaining burst time is more than the time quantum, it is placed at the back of the queue after execution.
- Continue until all processes complete.

---

## 🧾 Python Code
```python
def round_robin(processes, burst_time, time_quantum):
    n = len(processes)
    remaining_bt = burst_time[:]
    waiting_time = [0] * n
    turn_around_time = [0] * n
    completion_time = [0] * n
    t = 0  # current time
    done = False

    while not done:
        done = True
        for i in range(n):
            if remaining_bt[i] > 0:
                done = False
                if remaining_bt[i] > time_quantum:
                    t += time_quantum
                    remaining_bt[i] -= time_quantum
                else:
                    t += remaining_bt[i]
                    completion_time[i] = t
                    remaining_bt[i] = 0

    for i in range(n):
        turn_around_time[i] = completion_time[i]  # Arrival time is 0
        waiting_time[i] = turn_around_time[i] - burst_time[i]

    print("Processes  Burst Time  Completion Time  Waiting Time  Turn Around Time")
    for i in range(n):
        print(f"   {processes[i]} \t     {burst_time[i]} \t\t   {completion_time[i]} \t\t {waiting_time[i]} \t\t   {turn_around_time[i]}")

    avg_wt = sum(waiting_time) / n
    avg_tat = sum(turn_around_time) / n
    print(f"\nAverage Waiting Time = {avg_wt:.5f}")
    print(f"Average Turn Around Time = {avg_tat:.5f}")
