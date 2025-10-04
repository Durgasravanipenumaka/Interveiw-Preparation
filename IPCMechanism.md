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

## Message Queues :

### program :
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <unistd.h>

#define KEY 1234
#define SRVMSGTIME 1

struct msg {
    long mtype;
    pid_t pid;
    char text[100];
};

// Function to toggle case
void togglecase(char *str) {
    for (int i = 0; str[i]; i++) {
        if (islower(str[i])) str[i] = toupper(str[i]);
        else str[i] = tolower(str[i]);
    }
}

int main() {
    int msgid;
    struct msg m;

    // Create message queue
    msgid = msgget(KEY, IPC_CREAT | 0644);
    if (msgid == -1) {
        perror("msgget");
        exit(1);
    }

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        exit(1);
    } 
    else if (pid == 0) {
        // ----------- CLIENT PROCESS -----------
        sleep(1); // Give server time to start

        m.mtype = SRVMSGTIME;
        m.pid = getpid();

        printf("Client: Enter the text: ");
        scanf("%s", m.text);

        // Send message to server
        if (msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0) == -1) {
            perror("msgsnd");
            exit(1);
        }

        // Wait for response (mtype = pid)
        if (msgrcv(msgid, &m, sizeof(m) - sizeof(long), getpid(), 0) == -1) {
            perror("msgrcv");
            exit(1);
        }

        printf("Client: Response from server: %s\n", m.text);
    } 
    else {
        // ----------- SERVER PROCESS -----------
        while (1) {
            // Receive client request
            if (msgrcv(msgid, &m, sizeof(m) - sizeof(long), SRVMSGTIME, 0) == -1) {
                perror("msgrcv");
                continue;
            }

            printf("Server: Received from client %d: %s\n", m.pid, m.text);

            // Process message
            togglecase(m.text);

            // Send back to client (mtype = client pid)
            m.mtype = m.pid;
            if (msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0) == -1) {
                perror("msgsnd");
            }

            break; // exit after one message for simplicity
        }
    }

    // Cleanup (parent process deletes message queue)
    if (pid > 0) {
        msgctl(msgid, IPC_RMID, NULL);
    }

    return 0;
}
```

### client : 
```c
include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <unistd.h>
#include "common.h"

int main() {
    int msgid;
    struct msg m;

    msgid = msgget(KEY, 0);

    m.mtype = SRVMSGTIME;
    m.pid = getpid();

    printf("Enter the text: ");
    scanf("%s", m.text);

    msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0);

    // wait for response (mtype = pid)
    msgrcv(msgid, &m, sizeof(m) - sizeof(long), getpid(), 0);

    printf("Response: %s\n", m.text);
}
```
### server :
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <unistd.h>
#include "common.h"

void togglecase(char *str) {
    for (int i = 0; str[i]; i++) {
        if (islower(str[i]))
            str[i] = toupper(str[i]);
        else
            str[i] = tolower(str[i]);
    }
}

int main() {
    int msgid;
    struct msg m;

    msgid = msgget(KEY, IPC_CREAT | 0640);

    while (1) {
        // receive client request
        msgrcv(msgid, &m, sizeof(m) - sizeof(long), SRVMSGTIME, 0);

        togglecase(m.text);

        // send back to client, with mtype = client pid
        m.mtype = m.pid;
        msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0);
    }
}
```

