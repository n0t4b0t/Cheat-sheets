This cheat sheet mostly focuses on the enumeration commands. While I have included a few notes on what can be found etc, it's mostly intended as a reference for "what to check", assuming that the user has knowledge of what to do with the information returned.

| Command/file | Description |
| ---- | ---- |
| `hostname` | Returns hostname of target machine, which can sometimes reveal information about the system's role within a corporate network. |
| `uname -a` | Print system info giving additional details about the kernel used by the system. Search kernel version for vulnerabilities. |
| `/proc/version` | Contains info about system processes. May give info about kernel version and additional data like whether a compiler is installed. |
| `lspcu` | Show CPU info – some exploits require multiple cores. |
| `/etc/issue` | Contains info about OS, however, can be customised or changed |
| `ps (process status)` | Shows running processes. |
| `ps -A` | View all running processes. |
| `ps axjf` | View process tree. |
| `ps aux` | Shows processes for all users |
| `env` | Shows environmental variables. gives a bit more info about the system, some of it can be very useful. Have even found credentials in env in hackthebox before. |
| `sudo -l` | Lists all commands the current user can run using sudo. Check if they can lead to privilege escalation on GTFObins |
| `ls -la` | May be obvious, but use instead of plain ls. Shows hidden files/folders and their permissions. |
| `id` | Gives an overview of the user's privilege level and group memberships. Can also use `id` to obtain info about another user, e.g., `id Joel`. |
| `/etc/passwd` | Shows users on the system. I mostly pipe it to grep for user accounts with `cat /etc/passwd \| grep /bin/bash`, but it can be useful to look at the other accounts to see what services etc might be on the system. |
| `history` | Shows previous commands. Sometimes (rarely, but happens) contains credentials. Often disabled but give it a go. |
| `ifconfig` | Shows network connections. May be able to pivot to another device. |
| `netstat` | Can be used with several different options to gather information on existing connections: <br>`-a` = show listening ports and established connections<br>`-at` or `-au` = list TCP or UDP protocols respectively<br>`-l` = list ports in listening mode<br>`-s` = list network usage statistics by protocol<br>`-tp` = list connections with the service name and PID info<br>`-i`  = show interface statistics<br>`-ano` = display all sockets without resolving names |
| `/etc/crontab` | Shows scheduled tasks (cronjobs). Very common privilege escalation path in easy boxes on hackthebox. |
| `find` | Useful for searching the system for important information and potential privilege escalation vectors, e.g., `find / -size +100M -type f 2>/dev/null**` to find files larger than 100MB and redirect errors to `/dev/null`.<br>Note: **>2/dev/null** = very useful for error redirection in general. <br> |
| `find . name flag1.txt` | Find file named flag1.txt in current dir |
| `find /home –name flag1` | Finds file named flag1 in /home dir |
| `find / -type d –name config` | Find firectory named config under / |
| `find / -type f –perm 0777` | Find filer with the 777 permissions (files readable, writable, and executable by all users) |
| `find / -perm a=x` | Find executable files |
| `find /home –user frank` | Find files for user frank under /home |
| `find / -mtime 10` | Find files modified in the last 10 days |
| `find / -atime 10` | Find files that were accessed in the last 10 days |
| `find / -cmin -60` | Find files changed within the last hour (60mins) |
| `find / -amin -60` | Find files accessed in last hour (60min) |
| `find / -size 50M` | Find files with a 50MB size – can be used with + and – signs to specify files smaller or large than a given size, e.g. **find –size +100M** |
| `find / -writeable –type d 2>/dev/null` | Find world-writeable files |
| `find / -perm -222 –type d 2>/dev/null` | Find world writeable folders |
| `find / -perm –o w –type d 2>/dev/null` | Find world writeable folders – these 3 commands for the same result = because perm paramteter affects how find works. |
| `find / -perm –o x –type d 2>/dev/null` | Find world-executable folders |
| `find / -perm –u=s –type f 2>/dev/null` | Find files with SUID bit, which allows us to run the file with a higher privilege than the current user. GTFObins can be useful for exploiting these |
| Find development tools and supported languages: | `find / -name perl*`<br>`find / -name python*`<br>`find / -name gcc*`<br>etc |
