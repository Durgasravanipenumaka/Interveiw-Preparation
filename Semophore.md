## Semophore :
- A semaphore is a synchronization mechanism used in operating systems, multitasking, and embedded systems to manage access to shared resources among multiple processes or threads.
- It prevents conflicts like race conditions, which happen when two or more tasks try to access the same resource at the same time.
- 
### Types of Semaphores :
### 1. Binary Semaphore :
- Can have only 0 or 1.
- Used for mutual exclusion (mutex) or task synchronization.
- 0 → Resource unavailable/locked, 1 → Resource available/unlocked.
### Program :
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#include<semaphore.h>
int x=10;
sem_t binarysem;
void* task1(void* arg){
        for(int i=0;i<5;i++){
                sem_wait(&binarysem);
                x++;
                printf("Thread %ld incremented value to %d\n",(long)arg,x);
                sem_post(&binarysem);
        }
        return NULL;
}
void* task2(void* arg){
        for(int i=0;i<5;i++){
                sem_wait(&binarysem);
                x--;
                printf("Thread %ld decremented value to %d\n",(long)arg,x);
                sem_post(&binarysem);
        }
        return NULL;
}
int main(){
        pthread_t t1,t2;
        sem_init(&binarysem,0,1);
        pthread_create(&t1,NULL,task1,(void*)1);
        pthread_create(&t2,NULL,task2,(void*)2);
        pthread_join(t1,NULL);
        pthread_join(t2,NULL);
        sem_destroy(&binarysem);
}
```

### 2. Counting Semaphore :
- Can have a value 0, 1, 2, … N.
- 0 resource unavailable.
- >0 Number of resources available.
- Used when there are multiple instances of a resource.
- Example: A pool of 5 printers → semaphore initialized to 5.
### Program :
```c
#include<stdio.h>
#include<pthread.h>
#include<semaphore.h>
#include<unistd.h>
#define numoftasks 5
#define resources 2
sem_t countingsem;
void* task(void* arg){
        int id = *(int *)arg;
        printf("Task %d is waiting for resource\n",id);
        sem_wait(&countingsem);
        printf("Task %d acquired resource\n", id);
        sleep(2);
        printf("Task %d releasing resource\n", id);
        sem_post(&countingsem);
        return NULL;
}
int main(){
        pthread_t threads[numoftasks];
        int ids[numoftasks];
        sem_init(&countingsem,0,resources);
        for(int i=0;i<numoftasks;i++){
                ids[i]=i+1;
                pthread_create(&threads[i],NULL,task,&ids[i]);
        }
        for(int i=0;i<numoftasks;i++){
                pthread_join(threads[i],NULL);
        }
        sem_destroy(&countingsem);
}
```

### 3. Mutex (Mutual Exclusion) :
- A mutex is a binary semaphore with ownership.
- Only one thread/task can lock it at a time.
- The task that locks the mutex must unlock it.
- Used exclusively for mutual exclusion in critical sections.
- Binary in nature (0 = locked, 1 = unlocked).

### Program
```c
#include<stdio.h>
#include<pthread.h>
#include<unistd.h>
#define Numberoftasks 5
pthread_mutex_t lock;
void* task(void* arg){
        int id = *(int *)arg;
        printf("Task %d is waiting to enter critical section\n",id);
        pthread_mutex_lock(&lock);
        printf("Task %d is entered critical section\n",id);
        sleep(2);
        printf("Task %d leaving critical section\n",id);
        pthread_mutex_unlock(&lock);
        return NULL;
}
int main(){
        pthread_t threads[Numberoftasks];
        int ids[Numberoftasks];
        pthread_mutex_init(&lock,NULL);
        for(int i=0;i<Numberoftasks;i++){
                ids[i]=i+1;
                pthread_create(&threads[i],NULL,task,&ids[i]);
        }
        for(int i=0;i<Numberoftasks;i++){
                pthread_join(threads[i],NULL);
        }
        pthread_mutex_destroy(&lock);
}
```
