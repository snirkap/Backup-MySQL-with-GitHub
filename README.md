# Backup-MySQL-with-Git
I was tasked with backing up a large database while using the minimum amount of resources possible. I chose to use Git for this purpose because it's a method that consumes fewer resources. This is because Git only saves changes each time, instead of copying the entire dataset every time. Additionally, if I had used mysqldump, given the size of our database, performing backups during the day would have resulted in several minutes of downtime due to the volume of data being backed up each time. Ultimately, this approach would have required allocating more resources than the company was willing to.
## so this is how i do that:
1. first you need to do "git init" in the directory of the data
2. after that create a file that called git_commit.sh at /root/:
```
#!/bin/bash

# Change directory to /var/lib/mysql
cd /var/lib/mysql

# Add all files in the current directory to the staging area
git add .

# Commit the changes with a custom message that includes the current date and time
git commit -m "$(/bin/date +%Y-%m-%d-%H:%M).sql.bak"
```
3. chmod +x git_commit.sh
4. insert this command "/root/git_commit.sh" into crontab with this command and define how often you want the backup to happen: sudo crontab -u root -e
