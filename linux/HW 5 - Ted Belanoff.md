## Week 5 Homework Submission File: Archiving and Logging Data

Please edit this file by adding the solution commands on the line below the prompt.

Save and submit the completed file for your homework submission.

---

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives

1. Command to **extract** the `TarDocs.tar` archive to the current directory:

tar -xvvf TarDocs.tar

2. Command to **create** the `Javaless_Doc.tar` archive from the `TarDocs/` directory, while excluding the `TarDocs/Documents/Java` directory:

tar --exclude='./Documents/Java' -cvf .Javaless-Doc.tar -C ./TarDocs .

3. Command to ensure `Java/` is not in the new `Javaless_Docs.tar` archive:

tar --exclude "*/*/*/*" -tf Javaless-Doc.tar

**Bonus** 
- Command to create an incremental archive called `logs_backup_tar.gz` with only changed files to `snapshot.file` for the `/var/log` directory:

sudo tar -cvvWf ./logs_backup_tar.gz --listed-incremental=snapshot.file --level=0 ./log
sudo tar -cvvWf ./logs_backup_tar2.gz --listed-incremental=snapshot.file ./log

#### Critical Analysis Question

- Why wouldn't you use the options `-x` and `-c` at the same with `tar`?

One creates archives and one extracts archives. It does not make sense to be both archiving and dearchiving a set of files with tar at
the same time.

---

### Step 2: Create, Manage, and Automate Cron Jobs

1. Cron job for backing up the `/var/log/auth.log` file:

0 6 * * 3 sudo tar cvf ~/auth_backup.tgz ../../var/log/auth.log

---

### Step 3: Write Basic Bash Scripts

1. Brace expansion command to create the four subdirectories:


mkdir -p "backups/"{freemem,diskuse,openlist,freedisk}

2. Paste your `system.sh` script edits below:

    ```bash
    #!/bin/bash
	free -m > ~/backups/freemem/free_mem.txt
	du > ~/backups/diskuse/disk_usage.txt
    	lsof > ~/backups/openlist/open_list.txt
	df > ~/backups/freedisk/free_disk.txt
    ```

3. Command to make the `system.sh` script executable:

chmod +x system.sh

**Optional**
- Commands to test the script and confirm its execution:

sudo bash system.sh

**Bonus**
- Command to copy `system` to system-wide cron directory:

sudo cp system.sh > ../../etc/cron.d
---

### Step 4: Perform Various Log Filtering Techniques

1. Command to return `journalctl` messages with priorities from emergency to error:

journalctl (or journalctl -p 7)

2. Command to check the disk usage of the system journal unit since the most recent boot:

journalctl -b -u systemd-journald

3. Comand to remove all archived journal files except the most recent two:

journalctl --vacuum-file=2

**Bonus** 
- Command to filter all log messages with priority levels between zero and two, and save output to `/home/sysadmin/Priority_High.txt`:

journalctl -p 2 > '/home/sysadmin/Priority_High.txt'

- Command to automate the last command in a daily cronjob:


- Add the edits made to the crontab file below:

    ```bash
    [Your solution cron edits here]
    ```

---

### Step 5. Create Priority-Based Log Files

1. Command to record all mail log messages, except for debug, to `/var/log/mail.log`:


    - Add the edits made to the configuration file below:

    ```bash
    mail.!=debug 		-/var/log/mail.log
    ```

This involved changing 

mail.* 		-/var/log/mail.log

to

mail.!=debug 		-/var/log/mail.log

in the /etc/rsyslog.d/50-default.conf file.

**Bonus**

- Command to record all boot log messages, except for info and debug, to `/var/log/boot.log`:

    - Add the edits made to the configuration file below:

    ```bash
    [Your solution edits here]
    ```

---

### Step 6. Manage Log File Sizes
 
1. Run `sudo nano /etc/logrotate.conf` to edit the `logrotate` configuration file. 

    Configure a log rotation scheme that backs up authentication messages to the `/var/log/auth.log`.

    - Add your config file edits below:

    ```bash
    .var/log/auth.log{
	missingok
	rotate 7
	weekly
	notifempty
	compress
	delay compress
	endscript
}

`
    ```

---

### Bonus: Check for Policy and File Violations

1. Command to verify `auditd` is active:

2. Command to set number of retained logs and maximum log file size:

    - Add the edits made to the configuration file below:

    ```bash
    [Your solution edits here]
    ```

3. Command using `auditd` to set rules for `/etc/shadow`, `/etc/passwd` and `/var/log/auth.log`:


    - Add the edits made to the `rules` file below:

    ```bash
    [Your solution edits here]
    ```

4. Command to restart `auditd`:

5. Command to list all `auditd` rules:

6. Command to produce an audit report:

7. Create a user with `sudo useradd attacker` and produce an audit report that lists account modifications:

8. Command to use `auditd` to watch `/var/log/cron`:

9. Command to verify `auditd` rules:

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
