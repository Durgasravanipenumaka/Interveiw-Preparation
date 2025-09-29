## PIPE :
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>
#include<string.h>
int main(){
        int fd[2];
        int pid;
        char writemsg[]="Hello from parents!";
        char readmsg[100];
        pipe(fd);
        pid=fork();
        if(pid==0){
                close(fd[1]);
                read(fd[0],readmsg,sizeof(readmsg));
                printf("Child received:%s\n",readmsg);
                close(fd[0]);
        }
        else{
                close(fd[0]);
                write(fd[1],writemsg,strlen(writemsg)+1);
                close(fd[1]);
        }
}
```
