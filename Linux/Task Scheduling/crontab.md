
```bash
* * * * *   command to execute
- - - - -
| | | | |
| | | | +---- Day of the week (0 - 7) (Sunday=0 or 7)
| | | +------ Month (1 - 12)
| | +-------- Day of the month (1 - 31)
| +---------- Hour (0 - 23)
+------------ Minute (0 - 59)
```

|Command/Expression|Description|
|---|---|
|`crontab -e`|Edit the user's `cron` table.|
|`crontab -l`|View the user's `cron` table.|
|`crontab -r`|Remove the user's `cron` table.|
|`* * * * *`|Minute, Hour, Day of Month, Month, Day of Week|
|`0 2 * * 1-5`|Run at 2 AM on weekdays.|
|`*/15 * * * *`|Run every 15 minutes.|
|`@reboot`|Run at system startup.|
|`@yearly`|Run once a year at midnight of January 1.
#### Examples

```bash
#!/bin/bash
# Example cron jobs

# Run a script every hour
0 * * * * /path/to/script.sh

# Run a script every day at midnight
0 0 * * * /path/to/script.sh

# Run a script every Sunday at 4:30 AM
30 4 * * 0 /path/to/script.sh

# Run a script every 15 minutes
*/15 * * * * /path/to/script.sh

# Run a script every weekday at 8:00 AM
0 8 * * 1-5 /path/to/script.sh

# Run a script every 30th minute of every hour
30 * * * * /path/to/script.sh

# Run a script every 3 hours
0 */3 * * * /path/to/script.sh

# Run a script every 2nd day of the month at 6:00 PM
0 18 2 * * /path/to/script.sh

# Run a script every Monday and Thursday at 10:00 PM
0 22 * * 1,4 /path/to/script.sh

# Run a script every 10 minutes during business hours (9 AM to 5 PM) on weekdays
*/10 9-17 * * 1-5 /path/to/script.sh

```
    