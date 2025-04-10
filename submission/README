# CSC 453 Program 0 Writeup

## Ansh Pandey

### Part 0: Repeating Forks:
When running the fork_loop executable a handful of times I noticed something interesting. The amount of “Yo”’s followed by a number that is produced isn’t always the same. For me it varies between:
0Yo1YoYo2YoYoYo3YoYoYoYo4YoYoYoYoYo5YoYoYoYoYo5
0Yo1YoYo2YoYoYo3YoYoYoYo4YoYoYoYoYo5
I believe that the second string is the desired output as the way that the code function is that when the section with the loop is executed, it forks the parent process (as long as i < 5) and each process will print out an i number of “Yo”s followed by the value of i due to the way the buffer  is being built as the process forks. In other words, when you fork, the process memory image is duplicated, including the buffer so there are more ‘Yo’s that are printed as the program goes on. For the first output, it only happens occasionally and my assumption is that it has to do with the scheduler and how it prioritizes how the order that the parent and final child are run.

My fundamental understanding didn’t change, it just solidified the idea that as the program forks, an i number of ‘Yo’s is outputted followed by the value of i because of the way that the buffer builds as the child forks.

### Part 1: Who Runs First?
Initial observation based on given code: just because the parent process was spun up first, it doesn’t mean that it will terminate before the child does. In fact, more often than not the child process is run before the parent. This might be because of the way that the OS prioritizes child processes and any overhead that might be part of the forking process. Another big factor is probably the sleep() that is triggered for one second, causing the process to change states and, thus, the scheduler to switch what is actively running. 

printf() only -> Always says ‘Parent’ expect for the first one (says ‘child parent’) and the numbers are all out of order but they always add up to 1000

printf() and fflush() -> Always says ‘parent child’, the parent value is always 1, but the child values are different and not in order.

write() only -> just outputs ‘1000 parentchild’

I believe that this is due to differences in the way that the printf and write methods work. With write being a direct system call, it doesn’t have the artifacts left over from the print buffering so it is a much cleaner and more predictable process. The program with fflush() prior to the print attempts to clean the buffer before printing (which I think is why the value is always ‘1’ for the parent) but the child inherits the parent’s state, causing the variation in the child id. Finally for just the print() program, when the fork() happens, it copies the entire process including the buffer and the numbers add up to 1000 because each process pair represents one iteration so the parent gets 1000-i and the child gets i.

With a sleep time of 0.1 seconds there is a warning at compile time for converting a double to an unsigned int and the output is the same as if there was no sleep time. When sleep time is increased to 1 second (as it was in the provided code), the longer sleep affects the scheduler so the child process finishes before the parent in 990 out of 1000 cases.

### Part 2: 64- and 32-bit Process Memory Images

What is displayed by the computer is the virtual memory that is allocated to allow the program to run. It provides information about the process's stack, the heap, the text and data zones associated with the process. It reinforces the idea of the process being pretty isolated and not being directly in the the physical memory of the device. What I am unsure about is what the shared memory and dirty memory is. My best assumption is that shared memory is where the overhead for all processes are stored. It is a bit like the reserved storage on the physical storage for the OS. As for dirty memory, I would assume that it relates to information that needs to be cleaned up by the system’s garbage collector or information that the process has updated but it hasn’t been stored in physical memory or someplace else more permanently. 

### Additional Information

For each of the steps in Part 1, I made changes and complied them into different versions and rerouted the output into .txt files if you want to take a look I can send them over as well.
