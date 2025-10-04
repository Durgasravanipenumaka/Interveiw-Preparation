## 1.PIPE :
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

## 2.Message Queues :
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

## 3.Direct Task Notification Example using Threads :
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
pthread_cond_t cond = PTHREAD_COND_INITIALIZER;

char message[100];
int notified = 0; // flag for notification

void* server_task(void* arg) {
    sleep(1); // simulate work
    pthread_mutex_lock(&lock);

    // Prepare message
    snprintf(message, sizeof(message), "Hello from server task!");

    // Directly notify client
    notified = 1;
    pthread_cond_signal(&cond);

    pthread_mutex_unlock(&lock);
    printf("Server: Notification sent to client.\n");

    return NULL;
}

void* client_task(void* arg) {
    pthread_mutex_lock(&lock);

    // Wait for direct notification
    while (!notified) {
        pthread_cond_wait(&cond, &lock);
    }

    printf("Client: Received notification with message: %s\n", message);

    pthread_mutex_unlock(&lock);
    return NULL;
}

int main() {
    pthread_t server, client;

    pthread_create(&client, NULL, client_task, NULL);
    pthread_create(&server, NULL, server_task, NULL);

    pthread_join(server, NULL);
    pthread_join(client, NULL);

    return 0;
}
```

## 4.Mailbox :
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <unistd.h>
#include <ctype.h>

#define KEY 1234
#define SRVMSGTIME 1

struct msg {
    long mtype;
    pid_t pid;
    char text[100];
};

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
        sleep(1); // give server time to start

        m.mtype = SRVMSGTIME;
        m.pid = getpid();

        printf("Client: Enter text: ");
        scanf("%s", m.text);

        msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0);

        // wait for server response (mtype = pid)
        msgrcv(msgid, &m, sizeof(m) - sizeof(long), getpid(), 0);

        printf("Client: Response from server: %s\n", m.text);
    } 
    else {
        // ----------- SERVER PROCESS -----------
        while (1) {
            msgrcv(msgid, &m, sizeof(m) - sizeof(long), SRVMSGTIME, 0);
            printf("Server: Received from client %d: %s\n", m.pid, m.text);

            togglecase(m.text);

            m.mtype = m.pid;
            msgsnd(msgid, &m, sizeof(m) - sizeof(long), 0);

            break; // exit after one message for simplicity
        }
    }

    // Cleanup (only parent removes queue)
    if (pid > 0) {
        msgctl(msgid, IPC_RMID, NULL);
    }

    return 0;
}
```

