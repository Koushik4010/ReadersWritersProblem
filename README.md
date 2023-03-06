# ReadersWritersProblem
##Problem Statement
Write starvation free pseudo code for the classical readers-writers problem.

##Starvation free solution
**Pseudocode:**
```
semaphore orderQueue;   //requests are preserved in order of arrival uses FIFO priority
semaphore accessResource;   //Mutual exclusion of reading and writing processes
semaphore readersMutex;   //Prevents race condition while readcount is updating

//All the above semaphores are intialised to 1

int readcount=0;   //Keep track of number of readers


Readers Process:

wait(orderQueue); //wait untill all the process arrived first are completed

wait(readersMutex);  //avoid the entering of other readers while updating the readcount
if(readcount==0){
    wait(accessResource); //access of the shared resource by readers, and the writers are blocked from accessing
}
readcount++;  //Updating the number of readers
signal(readersMutex);
signal(orderQueue);  //signal the processes that are in the waiting queue to execute

   //Reading is performed  by accessing the shared resource

wait(readersMutex);
readcount--;
if(readcount==0){
     signal(accessResource);  //signaling the writers to access the shared resource
}
signal(readersMutex);



Writers Process:

wait(orderQueue);  //wait untill all the process arrived first are completed
wait(accessResource);  //access of the shared resource by readers, and the writers are blocked from accessing


     //Writing is performed by accessing the shared resource
signal(orderQueue);
signal(accessResource);  //signaling the readers to access the shared resource
```


 
