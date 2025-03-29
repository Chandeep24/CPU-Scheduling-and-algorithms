                            Code of FCFS:

#include <stdio.h>
// First Come First Serve (FCFS) Scheduling
void fcfs_scheduling(int processes[], int n, int burst_time[]) {
    int waiting_time[n], turnaround_time[n];
    waiting_time[0] = 0;
    
    for (int i = 1; i < n; i++)
        waiting_time[i] = burst_time[i - 1] + waiting_time[i - 1];
    
    for (int i = 0; i < n; i++)
        turnaround_time[i] = burst_time[i] + waiting_time[i];
}
    return 0;
}

                              Code of SJF:

#include<stdio.h>
// Shortest Job First (SJF) Scheduling
void sjf_scheduling(int processes[], int n, int burst_time[]) {
    int waiting_time[n], turnaround_time[n], temp;
    
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (burst_time[i] > burst_time[j]) {
                temp = burst_time[i];
                burst_time[i] = burst_time[j];
                burst_time[j] = temp;
            }
        }
    }
    
    waiting_time[0] = 0;
    for (int i = 1; i < n; i++)
        waiting_time[i] = burst_time[i - 1] + waiting_time[i - 1];
    
    for (int i = 0; i < n; i++)
        turnaround_time[i] = burst_time[i] + waiting_time[i];
}
 return 0;
}

                                  Code of Round Robin:

#include<stdio.h>
// Round Robin Scheduling
void round_robin_scheduling(int processes[], int n, int burst_time[], int quantum) {
    int remaining_time[n], waiting_time[n], turnaround_time[n];
    for (int i = 0; i < n; i++) remaining_time[i] = burst_time[i];
    
    int time = 0, done;
    do {
        done = 1;
        for (int i = 0; i < n; i++) {
            if (remaining_time[i] > 0) {
                done = 0;
                int executed_time = (remaining_time[i] > quantum) ? quantum : remaining_time[i];
                time += executed_time;
                remaining_time[i] -= executed_time;
                
                if (remaining_time[i] == 0) {
                    turnaround_time[i] = time;
                    waiting_time[i] = turnaround_time[i] - burst_time[i];
                }
            }
        }
    } while (!done);
}
   return 0;
}
                                    Code of Priority:

#include<stdio.h>
// Priority Scheduling
void priority_scheduling(int processes[], int n, int burst_time[], int priority[]) {
    int waiting_time[n], turnaround_time[n], temp;
    
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (priority[i] > priority[j]) {
                temp = priority[i]; priority[i] = priority[j]; priority[j] = temp;
                temp = burst_time[i]; burst_time[i] = burst_time[j]; burst_time[j] = temp;
            }
        }
    }
    
    waiting_time[0] = 0;
    for (int i = 1; i < n; i++)
        waiting_time[i] = burst_time[i - 1] + waiting_time[i - 1];
    
    for (int i = 0; i < n; i++)
        turnaround_time[i] = burst_time[i] + waiting_time[i];
}
   return 0;
}
