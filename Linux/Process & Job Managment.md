### Process Management

| Task                                    | Command | Example                | Description                                                      |
| --------------------------------------- | ------- | ---------------------- | ---------------------------------------------------------------- |
| **Viewing Processes**                   | `ps`    | `ps -ef`               | Display information about processes                              |
| **Killing Processes**                   | `kill`  | `kill PID`             | Terminate processes by ID or name                                |
|                                         |         | `killall process_name` | Terminate all processes with the specified name                  |
|                                         | `pkill` | `pkill -9 firefox`     | Terminate processes based on name or attributes                  |
| **Background Processes**                | `&`     | `command &`            | Run command in the background                                    |
| **Foreground and Background Switching** | `fg`    | `fg %job_number`       | Brings the job with the specified job number to the foreground.  |
|                                         | `bg`    | `bg %job_number`       | Resumes the job with the specified job number in the background. |

### Job Management:

|Task|Command|Example|
|---|---|---|
|**Viewing Jobs**|`jobs`|`jobs`|
|**Foreground and Background Jobs**|`fg`|`fg %job_number`|
||`bg`|`bg %job_number`|
|**Suspending Jobs**|`Ctrl + Z`|(Press `Ctrl + Z` during process run)|

### Process States:

Processes in Linux can be in various states:

| State              | Description                                                                 |
| ------------------ | --------------------------------------------------------------------------- |
| **Running (R)**    | Currently executing or waiting to be executed.                              |
| **Stopped (T)**    | Stopped by a signal or by user intervention.                                |
| **Sleeping (S)**   | Sleeping, waiting for an event to complete.                                 |
|  **Zombie (Z)**    | Completed, but the parent process has not yet acknowledged its termination. |

### Process Control Signals:

| Signal         | Description                                 |
| -------------- | ------------------------------------------- |
| **`Ctrl + C`** | Interrupt (SIGINT) - Terminate the process. |
| **`Ctrl + Z`** | Stop (SIGTSTP) - Suspend the process.       |
| **`Ctrl + `**  | Quit (SIGQUIT) - Terminate and dump core.   |
| **`Ctrl + D`** | EOF (End-of-file) - Close input.            |
