## top
The top command is the traditional way to view your system’s resource usage and see the processes that are taking up the most system resources.
 Top displays a list of processes, with the ones using the most CPU at the top.
 
` top`
 
## ps
 The ps command lists running processes. The following command lists all processes running on your system:

 `ps -A`
 
## pstree

The pstree command is another way of visualizing processes. It displays them in tree format. So, for example, your X server and graphical environment would appear under the display manager that spawned them.

## kill

The kill command can kill a process, given its process ID. You can get this information from the ps -A, top or pgrep commands.

`kill PID`

## pgrep

Given a search term, pgrep returns the process IDs that match it. For example, you could use the following command to find Firefox’s PID:

`pgrep firefox`

## pkill & killall

`pkill firefox
killall firefox`

## renice

The renice command changes the nice value of an already running process. The nice value determines what priority the process runs with. A value of -19 is very high priority, while a value of 19 is very low priority. A value of 0 is the default priority.

The renice command requires a process’s PID. The following command makes a process run with very low priority:

`renice 19 PID`
