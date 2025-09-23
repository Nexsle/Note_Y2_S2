# High-level Description
----
ALGORITHM: Bank Queue Simulation

MAIN PROGRAM LOOP:
    initialise
    repeat
        if hasNextCustomer and (completionQueue.empty or 
           nextCustomer.arrivalTime <= nextCompletionTime.completionTime) then
            process_arrival
        else
            process_completion
        fi
    until arrival file is empty and customerQueue is empty and completionQueue is empty
    finish

PROCESS_ARRIVAL:
    if availableTeller exists then
        assign customer to teller
        add completion event to completionQueue
    else
        add customer to customerQueue
     fi
    load next customer from file

PROCESS_COMPLETION:
    remove completion event from completionQueue
    if customerQueue not empty then
        serve next customer from customerQueue
        add new completion event to completionQueue
    else
        mark teller as idle
     fi



# Complexity Analysis
---
## Time Complexity
- **Priority Queue Operation**: $O(\log n)$ for enqueue/dequeue, where n = queue size
- **Teller Assignment**: $O(t)$ where t = number of tellers
- **Overall Simulation**: $O(c \times(\log n+t))$ where c = number of customer
Justification: 

## Space Complexity
- **Priority Queues**: $O(n)$ where n = maximum queue size ($\leq 100$)
- **Teller Arrays**: O(t) where t is number of tellers
- **Overall**: $O(n+t)=O(n)$ since n >> t

# Data Structures Used
---
## Priority Queue 

- **Purpose**: Manages both customer waiting queue and teller completion events
- **Reason**: Provides O(log n) insertion/deletion with automatic ordering
- **Customer Queue**: Max-heap ordered by priority (3>2>1), then arrival time (earlier first)
- **Completion Queue**: Min-heap ordered by completion time (earliest first)


# Compilation
---
```
Compilation Command:
g++ -o simulation main.cpp Simulation.cpp PriorityQueue.cpp

Execution:
./simulation
Enter file name: a1-sample.txt
```
# Snapshot
---
![[Pasted image 20250917193503.png]]

# Outputs
---
```
=== Simulation with 1 teller(s) ===
=== Simulation Results ===
Teller 1 served: 100 customers
Total simulation time: 1282.57
Average service time per customer: 12.7983
Average waiting time per customer: 361.906
Maximum length of the queue: 57
Average length of the queue: 28.2173
Teller 1 idle rate: 0

=== Simulation with 2 teller(s) ===
=== Simulation Results ===
Teller 1 served: 52 customers
Teller 2 served: 48 customers
Total simulation time: 653.311
Average service time per customer: 12.7983
Average waiting time per customer: 60.3841
Maximum length of the queue: 22
Average length of the queue: 9.24279
Teller 1 idle rate: 0.0120883
Teller 2 idle rate: 0.020538

=== Simulation with 3 teller(s) ===
=== Simulation Results ===
Teller 1 served: 40 customers
Teller 2 served: 32 customers
Teller 3 served: 28 customers
Total simulation time: 531.161
Average service time per customer: 12.7983
Average waiting time per customer: 3.68287
Maximum length of the queue: 5
Average length of the queue: 0.693363
Teller 1 idle rate: 0.15296
Teller 2 idle rate: 0.190321
Teller 3 idle rate: 0.23176

=== Simulation with 4 teller(s) ===
=== Simulation Results ===
Teller 1 served: 36 customers
Teller 2 served: 25 customers
Teller 3 served: 24 customers
Teller 4 served: 15 customers
Total simulation time: 531.161
Average service time per customer: 12.7983
Average waiting time per customer: 0.25181
Maximum length of the queue: 1
Average length of the queue: 0.0474074
Teller 1 idle rate: 0.230122
Teller 2 idle rate: 0.253121
Teller 3 idle rate: 0.438945
Teller 4 idle rate: 0.647696
```

# Impact of Tellers on Efficiency
---
- Waiting time reduction
	- 1 teller: 361.9 mins average wait
	- 2 tellers: 60.4 minutes average wait (83% reduction)
	- 3 tellers: 3.7 minutes average wait (94% further reduction)
	- 4 tellers: 0.25 minutes average wait (93% further reduction)
- Queue Length Management
	- Maximum queue length decreases dramatically: 57 → 22 → 5 → 1
	- Shows diminishing returns: biggest improvement from 1→2 tellers
- Efficiency Analysis:
	- 1-2 tellers: System is undersized, customers experience long waits
	- 3 tellers: Balanced system, minimal waiting with reasonable utilization
	- 4 tellers: Over-capacity, very low waiting but high idle costs
The marginal improvement in customer wait time from 3 to 4 tellers may not justify the additional staffing cost given the high idle rate