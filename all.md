# All: mid and final

## File System Basics

* Creating files/dirs/symlinks

    * files:

    ```console
	$ touch <name>
    $ # or
	$ > <name>
    ```

    * dirs:

    ```console
    $ mkdir <name> 
	$ # for dir hierachies
	$ mkdir -p <name>/<name>/<name>/...
    ```

    * symlinks:

    ```console
	$ ln -s <dest> <shortcut_name>
    ```

* Copying/Moving/Renaming/Removing

    * copying:

    ```console
	$ cp <src> <dest> # -r/R for recursion
	$ cmp <file1> <file1> # check if two files are identical
	$ diff -r <dir1> <dir2> # check if two dirs are identical
    ```

    * moving/renaming:

    ```console
	$ mv <src> <dest>
    ```

    * removing:

    ```console
	$ rm -r/R -f  <path> # -r for recursion, -f for force (write protected files)
	$ rmdir <empty_dir>
    ```

* Searching files

    * indexed search:

    ```console
    $ updatedb
    $ locate <name>
    ```

    * exhaustive search:

    ```console
    $ find <starting_point> -name/-type/-size
    ```

* Searching tools

    * `whereis` (searches for all the paths coresponding to a tool/command - executable path and man page path):

    ```console
    $ whereis <tool_name>
    ```

    * `which` (searches for the executable path of a tool):

    ```console
    $ which <tool_name>
    ```

    * `type` (gets the tool type - shell builtin, external, alias):

    ```console
    $ type <tool_name>
    ```

* Archiving and compressing

    * `tar`:

	1. creation:
    
       ```console
       $ tar cvf <archive_name> <files>
       ```

	1. getting the contents:
    
        ```console
        $ tar tf <archive_name>
        ```
    1. unarchiving:

        ```console
        $ tar xvf <archive_name>
        ```

    1. extracting to a specific dir:

        ```console
        $ tar xvf <archive_name> --directory <dir>
        ```
	1. adding a file to an already existing archive:

        ```console
        $ tar rvf <archive_name> <file>
        ```

    * `zip`:

    1. creation:
    
       ```console
       $ zip <archive_name> <files>
       ```

	1. getting the contents:
    
        ```console
        $ zip -sf <archive_name>
        ```
    1. unarchiving:

        ```console
        $ unzip <archive_name>
        ```

    1. extracting to a specific dir:

        ```console
        $ unzip <archive_name> -d <dir>
        ```
	1. adding a file to an already existing archive:

        ```console
        $ zip -u <archive_name> <file>
        ```


## Processes
 
* `ps` (without arguments prints all the processes from the current shell)

    * all processes in the system:

    ```console
    $ ps -e
    ```

    * all processes in the system without the table header

    ```console
    $ ps -e --no-header
    ```

    * all processes but with multiple attributes:

    ```console
    $ ps -e -f
    ```

    * all processes belonging to the `student` user:

    ```console
    $ ps -u student
    ```

    * all processes that **do not** belong to the `student` user:

    ```console
    $ ps -N -u student
    ```

    * all processes that have the program image `sleep`:

    ```console
    $ ps -C sleep
    ```

    * all the processes sorted after the CPU percentage:

    ```console
    $ ps -o pid,cmd,%cpu,rss --sort %cpu
    ```

* `pgrep` (get pids based on process attributes)

   * get the pids of the processes belonging to `student` and `daemon`:

   ```console
   $ pgrep -u student,daemon
   ```

* `uptime` (gets the system load from the last 1, 5, 15 minutes)

* `nice`, `renice` (modify the process priority at load/run time)

    ```console
    $ nice/renice [-n] +/-10 <pid>
    ```

* `jobs` (gets background processes)

    ```console
    $ jobs
    $ fg/bg <index_from_jobs>
    ```

* `lsof` (get process file descriptors - maximum of 1024 fds)

* `kill`

    * list `kill` signals:

    ```console
    $ kill -l
    1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
    6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
    11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
    16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
    21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
    26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
    31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
    38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
    43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
    48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
    53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
    58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
    63) SIGRTMAX-1  64) SIGRTMAX
    ```

    * kill process using `SIGKILL`:

    ```console
    $ kill -9 <pid>
    ```

* `pkill` (kills processes based on common attributes)

    * kill based on process user:

    ```console
    $ pkill -u <username>
    ```

    * kill based on parent pid:

    ```console
    $ pkill -P <ppid>
    ```

* Chaining commands based on exit code

    * getting the shell pid:

    ```console
    $ echo $$
    ```

    * getting the exit code of the last process of the shell:

    ```console
    $ echo $?
    ```

    * `||` (equivalent to `or`; executes commands until it finds one that succeeds):

    ```console
    $ comm1 || comm2 # comm2 gets executed only if comm1 fails
    ```

    * `&&` (equivalent to `and`; executes commands until it finds one that fails):

    ```console
    $ comm1 && comm2 # comm2 gest executed only if comm1 succeeds
    ```

    * `|` (pipes transfer the output of the last command as the input to the second command):

    ```console
    $ cat file | grep "a" # the output of the cat command was transfered as input to grep
    ```

* Services/Daemons

    * `systemctl` (diverse info about whatever executes on the system)

        * active services:

        ```console
        $ systemctl --type=service --state=active
        ```

        * active daemons:

        ```console
        $ systemctl | grep daemon
        ```