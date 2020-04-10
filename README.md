# Safe-or-unsafe-state-of-processe
24) In this question there are 5 process P0,P1,P2,P3,P4 To find whether the system is in safe  state or not,we implemented a code here which follows bankers algorithm,safe state algorithm and request resource algorithm
CODE:

#include<stdio.h> void Need(int need[5][4], int max[5][4],

int allot[5][4]) 

{ 

          for (int i = 0 ; i < 5 ; i++) 
	  
              for (int j = 0 ; j < 4 ; j++) 
	      
                         need[i][j] = max[i][j] - allot[i][j]; 
			 
} 

void isSafe(int processes[5],int avail[4],int max[5][4],int allot[5][4]) 

{ 

              int need[5][4]; 
	      
Need(need, max, allot);

int finish[5] = {0,0,0,0,0}; 

int safeSeq[5]; 

int work[4]; 

       for (int i = 0; i < 4 ; i++) 
       
            work[i] = avail[i]; 
	    
                       int count = 0;
		       
while (count < 5) 

   {          
   
              int found = 0;
	      
     for (int p = 0; p < 5; p++) 
     
      { 
		   
                          if (finish[p] == 0) 
			  
           { 
			 
int j; 

for (j = 0; j < 4; j++) 

if (need[p][j] > work[j]) 

   break; 
   
if (j == 4)

{ 

for (int k = 0 ; k < 4 ; k++) 

  work[k] += allot[p][k]; 
  
  safeSeq[count++] = p; 
  
  finish[p] = 1;
  
  found = 1; 
  
  } 
					   
        } 
	     
              } 
		       
                              if (found == 0) 
			      
              { 
		  
                             printf("System is not in safe state\n");
			     
                             return;
			     
             }
	
      } 
                
		printf("System is in safe state\n");  
		
       return; 
       
} 

void main() 

{ 

     int processes[5] = {0,1,2,3,4};
     
     int avail[4] = {1,5,2,0}; 
     
     int max[5][4] = {{0,0,1,2},{1,7,5,0},{2,3,5,6},{0,6,5,2},{0,6,5,6}}; 
     
     int allot[5][4] = {{0,0,1,2},{1,0,0,0},{1,3,5,4},{0,6,3,2},{0,0,1,2}};
     
     isSafe(processes,avail,max,allot); 
     
     return;
     
} 


In terms of Operating system concept:-
The banker’s algorithm could be a resource allocation and deadlock avoidance algorithm that tests for safety by simulating the allocation for predetermined maximum possible amounts of all resources, then makes an “s-state” check to check for possible activities, before deciding whether allocation should be allowed to continue.
Banker’s algorithm is known as so because it's employed in banking industry to test whether loan may be sanctioned to an individual or not. Suppose there are n number of account holders during a bank and therefore the total sum of their money is S. If an individual applies for a loan then the bank first subtracts the loan amount from the whole money that bank has and if the remaining amount is larger than S then only the loan is sanctioned. it's done because if all the account holders involves withdraw their money then the bank can easily have it off.
Following Data structures are used to implement the Banker’s Algorithm:

Let ‘n’ be the number of processes in the system and ‘m’ be the number of resources types.

Available : 
It is a 1-d array of size ‘m’ indicating the number of available resources of each type.
     Available[ j ] = k means there are ‘k’ instances of resource type Rj
Max :
It is a 2-d array of size ‘n*m’ that defines the maximum demand of each process in a system.
Max[ i, j ] = k means process Pi may request at most ‘k’ instances of resource type Rj.
Allocation :
It is a 2-d array of size ‘n*m’ that defines the number of resources of each type currently allocated to each process.
Allocation[ i, j ] = k means process Pi is currently allocated ‘k’ instances of resource type Rj
Need :
 It is a 2-d array of size ‘n*m’ that indicates the remaining resource need of each process.
Need [ i,   j ] = k means process Pi currently need ‘k’ instances of resource type Rj
for its execution.
Need [ i,   j ] = Max [ i,   j ] – Allocation [ i,   j ]



Additional Algorithm:-
Safety Algorithm:
Let Work and Finish be vectors of length ‘m’ and ‘n’ respectively.
Initialize: Work = Available
Finished[j] = false; for j=1, 2, 3, 4….n
2)Find  j that both
a) Finished[j] = false
b) Needi <= Work
if no such j exists goto step (4)
3) Work = Work + Allocation[j]
Finish[ j] = true
goto step (2)
4) if Finished [j] = true for all j
then the system is in a safe state

Resource-Request Algorithm:-
1) If Req <= Need
Goto step (2) ; otherwise, raise an error condition, since the process has exceeded its maximum claim.
2) If Req<= Available
Goto step (3); otherwise, P must wait, since the resources are not available.
3) Have the system pretend to have allocated the requested resources to process Pi by modifying the state as
follows:
Available = Available – Req
Allocation = Allocation + Req
Need= Need– Req




Constraints and results:

if there are 5 processes, P0 to P4, and 4 kinds of resources. At T0 we have the system state as follows: Max Instances of Resource Type A = 3 (2 allocated + 1 Available) Max 

Instances of Resource Type B = 14(9 allocated + 5 Available) Max Instances of Resource Type C = 12 (10 allocated + 2 Available) Max Instances of Resource Type D = 12 (12 allocated + 0 Available)

                                                                 GIVEN MATRICES
	Allocation Matrix (N0 of the allocated resources By a process)	Max Matrix Max resources that may be used by a process	Available Matrix Not Allocated Resources
	A	B	C	D	A	B	C	D	A	B	C	D
P0	0	0	1	2	0	0	1	2	1	5	2	0
P1	1	0	0	0	1	7	5	0				
P2	1	3	5	4	2	3	5	6				
P3	0	6	3	2	0	6	5	2				
P4	0	0	1	4	0	6	5	6				
Total	2	9	10	12								


1.	Create the need matrix (max-allocation)
       Need Matrix = Max Matrix – Allocation Matrix
   	A	B	C	D
P0	0	0	0	0
P1	0	7	2	1
P2	1	0	0	2
P3	0	0	2	0
P4	0	6	4	2
	
                                                                               




2. Use the safety algorithm to test if the system is in a safe state or not? 
a. We will first define work and finish:
                           Finish matrix	 Work vector
1	5	2	0
P0	False
P1	False
P2	False
P3	False
P4	False
Initially work = available = ( 1, 5 , 2, 0)
 Finish = False for all processes	




b. Check the needs of each process [ needs(pi) <= Max(pi)], if this condition is true: 
• Execute the process , Change Finish[i] =True 
• Release the allocated Resources by this process 
• Change The Work Variable = Allocated (pi) + Work
need0 (0,0,0,0) <= work(1,5,2,0) 
                           Finish matrix	 Work vector
1	5	3	2
P0-1	True
P1	False
P2	False
P3	False
P4	False
P0 will release the allocated P0 will be resources(0,0,1,2) executed because Work = Work need(P0) <= 
Work (1,5,2,0)+Allocated(P0) 
P0 will be True (0,0,1,2)=1,5,3,2
Need1 (0,7,5,0) <= work(1,5,3,2) Condition Is False P1 will Not be executed Need2 (1,0,0,2)<=work(1,5,3,2) so P2 will be executed.
The processes are executed and The system is in safe state with execution process is P0,P2,P3,P4,P1.

Complexity of the program:-  n^3 
