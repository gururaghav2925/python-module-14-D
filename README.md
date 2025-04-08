#  Round Robin Scheduling Algorithm in Python

## Aim
To calculate:- Completion Time, Turn Around Time (TAT), Waiting Time (WT)
for multiple processes using **Round Robin Scheduling**, where all arrival times are 0.

---

##  Procedure

1. **Initialize Inputs:**
   - Get the list of process IDs and their corresponding burst times.
   - Set a fixed time quantum for the scheduler.
   - Assume all arrival times are 0.

2. **Set Up Tracking:**
   - Use arrays to track remaining burst time, completion time, waiting time, and turnaround time.
   - Initialize a `current_time` variable to simulate CPU time.

3. **Simulate Round Robin Execution:**
   - Loop through the processes repeatedly in order.
   - For each process:
     - If its remaining time is more than the quantum, reduce it and increase the current time.
     - If its remaining time is less than or equal to the quantum, finish it, set its completion time, and mark it as done.
   - Continue until all processes are complete.

4. **Calculate Final Metrics:**
   - Turn Around Time = Completion Time - Arrival Time (arrival time is 0)
   - Waiting Time = Turn Around Time - Burst Time

5. **Display Output:**
   - Print a table showing each process with its Burst Time, Completion Time, Turn Around Time, and Waiting Time.
   - Compute and display the average waiting and turnaround times.

---

##  Python Code
```python
# Python3 program for implementation
# of FCFS scheduling

# Function to find the waiting
# time for all processes
def findWaitingTime(processes, n,
					bt, wt):

	# waiting time for
	# first process is 0
	wt[0] = 0

	# calculating waiting time
	for i in range(1, n ):
		wt[i] = bt[i - 1] + wt[i - 1]

# Function to calculate turn
# around time
def findTurnAroundTime(processes, n,
					bt, wt, tat):

	# calculating turnaround
	# time by adding bt[i] + wt[i]
	for i in range(n):
		tat[i] = bt[i] + wt[i]

# Function to calculate
# average time
def findavgTime( processes, n, bt):

	wt = [0] * n
	tat = [0] * n
	total_wt = 0
	total_tat = 0

	# Function to find waiting
	# time of all processes
	findWaitingTime(processes, n, bt, wt)

	# Function to find turn around
	# time for all processes
	findTurnAroundTime(processes, n,
					bt, wt, tat)

	# Display processes along
	# with all details
	print( "Processes Burst time " +
				" Waiting time " +
				" Turn around time")

	# Calculate total waiting time
	# and total turn around time
	for i in range(n):
	
		total_wt = total_wt + wt[i]
		total_tat = total_tat + tat[i]
		print(" " + str(i + 1) + "   " +
					str(bt[i]) + "  " +
					str(wt[i]) + "    " +
					str(tat[i]))

	print( "Average waiting time = "+
				str(total_wt / n))
	print("Average turn around time = "+
					str(total_tat / n))

# Driver code
if __name__ =="__main__":
	
	# process id's
	processes = [ 1, 2, 3]
	n = len(processes)

	# Burst time of all processes
	t0=int(input())
	t1=int(input())
	t2=int(input())
	burst_time = [t0,t1,t2]

	findavgTime(processes, n, burst_time)
```
## Output:
![image](https://github.com/user-attachments/assets/54deadce-368d-4a95-8f8c-a454fe315acd)

## Result:
The program successfully implements the Round Robin scheduling algorithm and computes all relevant times as expected.

