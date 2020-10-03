
# What is supervisor?
Supervisor is a client/server system that allows its users to control a number of processes on Linux and UNIX-like operating systems. Processes can be grouped into “process groups” and a set of logically related processes can be stopped and started as a unit. It starts its subprocesses via fork/exec and subprocesses don’t daemonize. The operating system signals Supervisor immediately when a process terminates.

Supervisor is based on four components:

supervisord: It is the server piece which is responsible for starting child programs at its own invocation, responding to commands from clients, restarting crashed or exited subprocesseses.
supervisorctl: it is the command-line client piece which provides a shell-like interface to the features provided by supervisord. A user can connect to different supervisord processes, get status on the subprocesses controlled by, stop and start subprocesses of, and get lists of running processes of a supervisord



1) Install supervisor
Supervisor offers the possibility to be installed but I will show you the installation through distribution packages.

On centos 7

# yum install epel-release -y && yum update
````# yum install supervisor
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.linode.com
 * epel: fedora-epel.mirrors.tds.net
 * extras: mirrors.linode.com
 * updates: mirrors.linode.com
Resolving Dependencies
--> Running transaction check
---> Package supervisor.noarch 0:3.1.4-1.el7 will be installed
--> Processing Dependency: python-meld3 >= 0.6.5 for package: supervisor-3.1.4-1.el7.noarch
--> Processing Dependency: python-setuptools for package: supervisor-3.1.4-1.el7.noarch
On Ubuntu 16.04
```
# apt update && apt upgrade
```
# apt install supervisor
Reading package lists... Done
Building dependency tree 
Reading state information... Done
The following additional packages will be installed:
 python-meld3 python-pkg-resources
Suggested packages:
 python-setuptools supervisor-doc
The following NEW packages will be installed:
 python-meld3 python-pkg-resources supervisor
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 392 kB of archives.
2) Start with the monitoring tool supervisor
The supervisor configuration file is /etc/supervisord.conf. It is used both for supervisord and supervisorctl commands.
```


`# vim /etc/supervisor.conf
[unix_http_server]
file=/var/run/supervisor/supervisor.sock ; (the path to the socket file)
;chmod=0700 ; sockef file mode (default 0700)
;chown=nobody:nogroup ; socket file uid:gid owner
;username=user ; (default is no username (open server))
;password=123 ; (default is no password (open server))`

# vim /etc/supervisord.conf
[program:cat-command]
command=/bin/cat ; the program (relative uses PATH, can take args)
process_name=%(program_name)s ; process_name expr (default %(program_name)s)
numprocs=1 ; number of processes copies to start (def 1)

[program:apache2]
command=/usr/sbin/httpd -c "ErrorLog /dev/stdout" -DFOREGROUND
redirect_stderr=true
c) Start supervisord
To start supervisord, we will run supervisord command. For the first time, You can use the -n option to launch it in the foreground which is useful to debug startup problems and the -c flag to indicate the full path of the configuration file. The resulting process will daemonize itself and detach from the terminal. It keeps operations log at /var/log/supervisor/supervisord.log by default. If you don't use the -c, supervisord will first search the configuration in the current folder

# supervisord -c /etc/supervisord.conf
Now we can check the supervisor log file

3) Monitor your processes with supervisor
We can use the web interface to manage the processes with supervisor or we can use thesupervisorctl command line. We have configured two processes but one process doesn't work well, so we will see how supervisor will check our processes

a) Monitor the process with supervisorctl
supervisorctl use some basics commands to manage your processes: stop, start, status, restart, reload, tail, etc.. To manage your process, use the supervisorctl command

You can restart the process with the command below

# supervisorctl restart all
`cat-command: stopped
cat-command: started
apache2: ERROR (abnormal termination)`