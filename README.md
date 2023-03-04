# Starve_free_Readers-Writers-Problem
Readers Writers Problem is a classic synchronization problem in Operating Systems. It involves readers and writers trying to read or edit a document simultaneously which can lead to one or more writers simultaneously modifying information could lead to errors in documents. So, here too like other problems, the three conditions should hold to solve the race condition namely, mutual exclusion, progress and bounded waiting.
# Pseudocode
```cpp
/*Starting Section*/
wait(enter)
rdcount++;
if(rdcount==1) wait(write);
signal(enter)
*/Critical Section*/
wait(exit)
rdcount--;
if(rdcount==0) signal(write);
signal(exit)
/*Remainder Section*/
```
