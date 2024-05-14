
| Action          | Command                       |
| --------------- | ----------------------------- |
| Start service   | `systemctl start <service>`   |
| Stop service    | `systemctl stop <service>`    |
| Restart service | `systemctl restart <service>` |
| Enable on boot  | `systemctl enable <service>`  |
| Disable on boot | `systemctl disable <service>` |
| Reload config   | `systemctl reload <service>`  |
| Check status    | `systemctl status <service>`  |

### Service states

| State            | Description                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------- |
| Active (running) | The service is currently running and its main process is active.                               |
| Active (exited)  | The service has been started successfully and has completed its execution, but is not running. |
| Inactive         | The service is not running and has not been started.                                           |
| Activating       | The service is in the process of starting.                                                     |
| Deactivating     | The service is in the process of stopping.                                                     |
| Failed           | The service failed to start or encountered an error during execution.                          |
| Reloading        | The service is reloading its configuration.                                                    |
| Waiting          | The service is waiting for a particular event or condition before starting or stopping.        |
| Starting         | The service is in the process of starting, but its main process has not yet been activated.    |
| Stopping         | The service is in the process of stopping, but its main process is still active.               |
