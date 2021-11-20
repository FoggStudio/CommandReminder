# Linux
## General
Moving to precedent directory: `cd -`  
Using previous command with sudo: `sudo !!`

## Disk information
Get readable information : `df -ha`  
Sizes of files and subdirectories in the current folder, in descending order of size :  
`du -a --max-depth=1 | sort -nr`  
Current directory size : `du -hs .`  
Current directory files with size : `ls -lh`  
Find modified file between two date : `find . -type f -newermt "aaaa-mm-jj hh:mm:ss" ! -newermt "aaaa-mm-jj hh:mm:ss"`
Change file modified timestamp in metadata :  `touch -m -t <timestamp> <file> ` Timestamp format looks like this : `[[CC]YY]MMDDhhmm[.ss]`

## Network information
Get ip addresses : `hostname -I`  
Get network interfaces : `ip a`  or `ip link show`  
Get DNS informations : `cat /etc/resolv.conf` or `grep "nameserver" /etc/resolv.conf`    
Get gateways information : `ip r` or `ip r | grep default`  
Activate or deactivate a network interface: 
```bash
ip link set <ethernet interface> up
ip link set <ethernet interface> down
```
Change network information : `vi /etc/netplan/*.yaml` then apply with `netplan apply`

## Process Information
Sort by memory usage: `ps aux | sort -nk 4`  
Sort by cpu usage: `ps aux | sort -nk 3`  

## Archive files
`tar -czvf name-of-archive.tar.gz /path/to/directory-or-file` (Could add multiples directories or files)

## Delete files
Keep only the X most recent files in a folder: `ls -1t | tail -n +11 | xargs rm -f`  
Delete files older than 30 days: `find /opt/backup -type f -mtime +30 -delete`  
Delete files with a specific extention older than 30 days: `find /var/log -name "*.log" -type f -mtime +30 -delete`  
Delete files recursively older than 30 days: `find /var/log -type f -mtime +30 -exec rm -rf {} \;`  
Delete folders recursively older than 30 days: `find /var/log -type d -mtime +30 -exec rm -rf {} \;`  

## Display
Display as a table: `<command> | column -t`  
Replacing spaces with tabs: `<command> | tr ':[space]:' '\t'`