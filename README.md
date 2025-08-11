# Linux-IPC-Semaphores
Ex05-Linux IPC-Semaphores

# AIM:
To Write a C program that implements a producer-consumer system with two processes using Semaphores.

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - Sempahores

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## Write a C program that implements a producer-consumer system with two processes using Semaphores.
```
// C Program for Message Queue (Reader Process)
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

// structure for message queue
struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;
int main()
{
	key_t key;
	int msgid;
    	// ftok to generate unique key
	key = ftok("progfile", 65);
	// msgget creates a message queue
	// and returns identifier
	msgid = msgget(key, 0666 | IPC_CREAT);
	// msgrcv to receive message
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	// display the message
	printf("Data Received is : %s \n",
    		message.mesg_text);

    // to destroy the message queue
	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}
```

## OUTPUT
$ ./sem.o 

<img width="507" height="811" alt="445147665-1149af80-e3ad-4ee3-85f6-7cc552a6970e" src="https://github.com/user-attachments/assets/5778c5fe-ab6e-4676-833c-83c4181df021" />


$ ipcs


<img width="647" height="423" alt="445147685-f780a7e0-0ece-43ea-af84-82e632246cb2" src="https://github.com/user-attachments/assets/d9fe0845-94cc-4fb5-8570-2e75b00d2e5b" />



# RESULT:
The program is executed successfully.
