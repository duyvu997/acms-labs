### How to

To run a cron job on Ubuntu, you can use the built-in cron service. Here's a step-by-step guide on how to set up and run a cron job on Ubuntu:

1. Open a terminal:  
 
2. Edit the cron table:  
    To add a new cron job, use the crontab -e command. This will open the default text editor to edit the cron table for the current user.

    ```
    crontab -e
    ```
    If this is your first time setting up a cron job, you might be prompted to choose a text editor. Select your preferred editor, or simply follow the on-screen instructions.

3. Add the cron job:  
    In the editor, you'll see the cron table structure with examples at the bottom. Each line represents a cron job. To add a new cron job, add a line in the following format:

    ```
    * * * * * /path/to/your/command
    ```

    The five asterisks (*) represent the time when the cron job will run. Each asterisk corresponds to a specific time unit: minute, hour, day of the month, month, and day of the week. Replace /path/to/your/command with the actual command or script you want to run. For example, to run a script named "backup_script.sh" every day at 2 AM, the line would be:

    ```
    0 2 * * * /path/to/backup_script.sh
    ```

3. Save and exit:
    Save the changes and exit the editor. For example, in Nano, press Ctrl + X, then Y, then Enter.

4. Verify the cron job:  
    To verify that your cron job has been added successfully, you can list the current cron jobs using the command:

    ```
    crontab -l
    ```
    This will display the contents of your cron table, showing all the active cron jobs for your user.

5. Check the cron service status:  
    The cron service should be running by default on Ubuntu. You can check its status using the following command:

    ```
    systemctl status cron
    ```

    If the service is not running, you can start it with:

    ```
    sudo systemctl start cron
    ```
    That's it! Your cron job is now set up and will run automatically at the specified time according to the cron schedule. Remember to use absolute paths for commands and files in your cron job, as the cron environment might not have the same PATH settings as your interactive shell.

#### Notes:
- should use absolute paths
- check log: `cat /var/log/syslog | grep CRON`
- verify cron time: https://crontab.guru/#1/_*_*_*_*
- use pattern `* * * * * /path/to/your/command > /path/to/output.log 2>&1` to save the output. `>` for overwriting logs.
- use pattern `* * * * * /path/to/your/command >> /path/to/output.log 2>&1` to save the output. `>>` for appending logs.