# CIS*3050 Assignment 4 - Mini Grid: Shell, FIFO, and Sockets
## Kevin Sullivan



# Testing

## Brief Overview

The server output is stored in a file which is read from by `./runtests` and output to this file is compared to the expected output. Originally, the commands were executed in the script and compared to as substrings within the log files. Unfortunately, my implementation worked with `bash` but not `sh` which caused me to simplify my approach for test cases.

Terminal 1: `./mgServer > log/server.log`

Terminal 2: `./runtests`

**Note: If the test says a socket was not created, please repeat the above step.**

**Note: If an 'address already in use' error appears, delete the socket in /tmp/.**

## Cores
Tests for the existence of processing cores.

> Returns OK if there are more than 0 cores detected.

> Returns ERROR otherwise.
## Setup
Tests for the existence of the server FIFO.

> Returns OK if pipe is detected.

> Returns ERROR if not detected.

Tests for the existence of processor FIFO(s).

> Returns OK if pipe(s) detected.

> Returns ERROR if not detected.

Tests for the existence of the socket.

> Returns OK if socket detected.

> Returns ERROR if not detected.

## FIFO Commands
Tests the command `ls` on all available processors once.

> Returns OK if the command was successfully sent to the server (which then sends to the 
processors to be written)

> Returns ERROR otherwise

Tests the server status (jobs completed) which should be equal to the number of processors
> Returns OK if the jobs completed equals the number of cores

Tests the command `pwd` on all available processors once.

> Returns OK if the command was successfully sent to the server

> Returns ERROR otherwise

Tests the server status (jobs completed) which should be equal to 2 * number of processors

> Returns OK if the jobs completed equals 2 * number of cores

> Returns ERROR otherwise

## Socket Commands
Tests the command `ls -l` on all available processors once through `mgSubmitJob`.

> Returns OK if the command was successfully sent to the server

> Returns ERROR otherwise

Tests the shell script `timedCountdown` to verify that requests are queued as intended by a socket (sends more jobs than available processors)

> Returns OK if the amount of jobs received by the server reflects the number of jobs sent

> Returns ERROR otherwise

Tests the server status (jobs completed) which should be equal to 3 * number of processors + amount of times `timedCountdown` was called/

> Returns OK if the jobs completed equals 2 * number of cores + `timedCountdown` sum.

> Returns ERROR otherwise

Server shuts down by unbinding the socket, killing all processors, and the server.

**Log files contain a timestamp, command name, and the full command output.**