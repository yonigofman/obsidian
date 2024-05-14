
##### Create and edit your `.service` file. For example, you can use `vim` with the following command:

```
vim /etc/systemd/system/example.service
```
##### Write the Service Configuration. Here's an example of what you might include:

```ini
[Unit]
Description=My Example Service
After=network.target

[Service]
Type=simple
ExecStart=/path/to/your/executable
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

###### Here is expanded table with all available service configuration parameters:

| Section     | Parameter         | Description                                                                                                                                                        |
| ----------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `[Unit]`    | Description       | A human-readable description of the service.                                                                                                                       |
|             | Documentation     | Provides documentation for the service.                                                                                                                            |
|             | Requires          | Lists units that the service requires to function properly.                                                                                                        |
|             | RequiresMountsFor | Lists mount points for which the service requires mounted filesystems.                                                                                             |
|             | After             | Specifies when the service should be started in relation to other services. For example, `network.target` ensures that the service starts after the network is up. |
|             | Before            | Specifies services that should be started before this service.                                                                                                     |
|             | Conflicts         | Specifies units that this service conflicts with.                                                                                                                  |
|             | BindsTo           | Ensures that if this service is stopped, the listed unit will also be stopped.                                                                                     |
|             | PartOf            | Ensures that if this service is started, the listed unit will also be started.                                                                                     |
|             | OnFailure         | Specifies units that should be started if this service fails.                                                                                                      |
| `[Service]` | Type              | Specifies the process type. `simple`, `forking`, `oneshot`, `dbus`, `notify`, `idle`, or `exec` are common types.                                                  |
|             | ExecStart         | Specifies the command to start the service.                                                                                                                        |
|             | ExecStartPre      | Commands to execute before the main service is started.                                                                                                            |
|             | ExecStartPost     | Commands to execute after the main service is started.                                                                                                             |
|             | ExecReload        | Command to reload the service configuration.                                                                                                                       |
|             | ExecStop          | Command to stop the service.                                                                                                                                       |
|             | ExecStopPost      | Commands to execute after the service is stopped.                                                                                                                  |
|             | PIDFile           | Specifies the path to the process ID file.                                                                                                                         |
|             | WorkingDirectory  | Specifies the working directory for the service.                                                                                                                   |
|             | User              | Specifies the user account under which to run the service.                                                                                                         |
|             | Group             | Specifies the group account under which to run the service.                                                                                                        |
|             | Environment       | Sets environment variables for the service.                                                                                                                        |
|             | EnvironmentFile   | Specifies a file containing environment variables for the service.                                                                                                 |
|             | Restart           | Controls the restart behavior. `no`, `on-success`, `on-failure`, `on-abnormal`, `on-abort`, or `always` are common options.                                        |
|             | RestartSec        | Specifies the time to wait before restarting the service.                                                                                                          |
|             | TimeoutStartSec   | Specifies the time to wait for the service to start.                                                                                                               |
|             | TimeoutStopSec    | Specifies the time to wait for the service to stop.                                                                                                                |
|             | TimeoutSec        | Specifies the overall time limit for the service.                                                                                                                  |
|             | RemainAfterExit   | Specifies whether the service should be considered active after its main process exits.                                                                            |
|             | StandardInput     | Specifies where standard input should come from.                                                                                                                   |
|             | StandardOutput    | Specifies where standard output should go.                                                                                                                         |
|             | StandardError     | Specifies where standard error should go.                                                                                                                          |
|             | SyslogIdentifier  | Sets the identifier for messages sent to syslog.                                                                                                                   |
| `[Install]` | WantedBy          | Specifies the target that should be reached for this service to be started. `multi-user.target` means the service will start in multi-user mode.                   |
|             | RequiredBy        | Lists units that require this service to function properly.                                                                                                        |
|             | Alias             | Creates an alias for the service unit file.                                                                                                                        |

##### Reload systemd and Enable the Service.

```bash
sudo systemctl daemon-reload
```

Then, enable and start your service:

```bash
sudo systemctl enable example.service 
sudo systemctl start example.service
```
