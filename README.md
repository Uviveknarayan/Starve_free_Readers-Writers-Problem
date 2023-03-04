# Starve_free_Readers-Writers-Problem
Readers Writers Problem is a classic synchronization problem in Operating Systems. It involves readers and writers trying to read or edit a document simultaneously which can lead to one or more writers simultaneously modifying information could lead to errors in documents. So, here too like other problems, the three conditions should hold to solve the race condition namely, mutual exclusion, progress and bounded waiting.
# Formulation of the problem
There is a shared data between many users who perform reading and writing which could make the system faulty due to concurrency problems. So, we need to devise a ensure synchronization. Also, there are various solutions to this code in which the first readers writers solution, consists of starving the writers. The second Readers-Writers Problem gives priority to writers and the readers starve. In this repo, we are going to solve the readers writers problem such that both readers and writers don't starve.
Shared data
    -File, Database etc
 Semaphore
      -enter-mutual exclusion for processes entering and modifying rdcount and to ensure FIFO order too.
      -exit- mutual exclusion between readers while modifying shared rdcount variable
      -write- to provide mutual exclusion between reader and writer
Initially
      -enter=1,exit=1,write=1
      -rdcount=0 //keeps a track of readers reading presently
## Pseudocode
```cpp
typedef struct{
int val;
struct process *list;
}semaphore

wait(semaphore *s, int pid){
s->val--;
if(s->val<0){
add pid to s->list from end;                  //adding a process from the tail of list
block();
}
}

signal(semaphore *s){
s->val++;
if(s->val<=0){
remove a process from head of list from s->list;            //removing from head so that FIFO order is followed
wakeup(prid);
}
}
```
# Reader's Code
```cpp
/*Starting Section*/
wait(enter)
rdcount++;
if(rdcount==1) wait(write);
signal(enter)
/*Critical Section*/
//Perform Reading
wait(exit)
rdcount--;
if(rdcount==0) signal(write);
signal(exit)
/*Remainder Section*/
```
# Writer's Code
```cpp
/*Starting Section*/
wait(enter)
wait(write)
/*Critical Section*/
//Perform Writing
signal(write)
signal(enter)
/*Remainder Section*/
```
