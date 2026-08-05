# 18 Linux Commands Every Dev Must Know

Source: Instagram @coderz.py

## 1. grep

tags: `TEXT SEARCH`
Search text patterns across files instantly.

```
$ grep -r "TODO" ./src
src/api.py:42 # TODO: add retry
src/db.py:11 # TODO: pool size
```

finds every occurance of a pattern across a whole codebase.

## 2. find

tags: `FILE SEARCH`
Locate files by name, type, size or age.

```
$ find . -name "*.log" -mtime +7
./logs/app.log
./logs/error.log
```

hunts down files by name, type or how old they are.

## 3. chmod

tags: `PERMISSIONS`
Control who can read, write, or run a file.

```
$ chmod +x deploy.sh
-rwxr-xr-x deploy.sh
```

makes a script executable or locks a file down.

## 4. ps / top

tags: `PROCESSES`
See exactly what's running and how much it's using.

```
$ ps aux | grep node
u  4321  2.1  1.4  node server.js
```

shows every running processes and it's resource usage.

## 5. kill

tags: `PROCESSES`
Force-stop a process that won't quit on its own.

```
$ kill -9 4821
process 4821 terminated
```

sends a signal to stop or force-kill a stuck process.

## 6. curl

tags: `NETWORKING`
Poke an API without ever leaving the terminal.

```
$ curl -I https://api.example.com
HTTP/2 200
content-type: application/json
```

makes an HTTP request and shows you exactly what came back.

## 7. ssh

tags: `NETWORKING`
Get a secure shell on a remote machine.

```
$ ssh deploy@203.0.113.5
Welcome to Ubuntu 22.04 LTS
deploy@prod:~$
```

opens an encrypted remote shell on another machine.

## 8. tar

tags: `FILES`
Package and compress a whole directory at once.

```
$ tar -czvf backup.tar.gz ./data
data/
data/users.csv
data/config.json
```

bundles many files into one compressed archive.

## 9. df / du

tags: `DISK`
See what's actually eating your disk space.

```
$ df -h && du -sh ./node_modules
/dev/sda1 42G used 18G free
512M ./node_modules
```

shows free space on disks and size of specific folders.

## 10. ln -s

tags: `FILES`
Point one path at another without copying anything.

```
$ ln -s /opt/app/current /opt/app/live
live -> /opt/app/current
```

creates a shortcut path that always follows the real one.

## 11. sed

tags: `TEXT PROCESSING`
Find-and-replace text without opening an editor.

```
$ sed -i 's/foo/bar/g' config.yml
config.yml updated in place
```

edits text in a file or stream using a pattern.

## 12. awk

tags: `TEXT PROCESSING`
Pull just the columns you actually need from raw text.

```
$ awk '{print $1, $3}' access.log
10.0.0.4 /api/orders
10.0.0.4 /api/users
```

processes text column by column, built for log parsing.

## 13. xargs

tags: `TEXT PROCESSING`
Turn piped output into real command arguments.

```
$ find . -name "*.tmp" | xargs rm
removed 14 .tml files
```

feeds the output of one command as args to another.

## 14. lsof

tags: `NETWORKING`
Find out what process is hogging a port.

```
$ lsof -i :3000
node  4821  user  TCP *:3000  (LISTEN)
```

lists open files and network ports, and who owns them.

## 15. ss / netstat

tags: `NETWORKING`
See every open connection and listening port.

```
$ ss -tulpn
tcp  LISTEN  0.0.0.0:3000  node/4821
```

shows active connections and what's listening where

## 16. crontab -e

tags: `AUTOMATION`
Schedule a script to run on its own, forever

```
$ crontab -e
0 3 * * * /scripts/backup.sh
```

runs a command automatically on a recurring schedule.

## 17. systemctl

tags: `SERVICES`
Start, stop or check a background service.

```
$ systemctl restart nginx
nginx.service: active (running)
```

controls and inspects services managed by systemd

## 18. rsync

tags: `FILES`
Sync files fast, transferring only what changed.

```
$ rsync -avz ./build user@host:/var/www
sent 1.2MB received 340B
speedup: 8.4x
```

copies files locally or remotely, skipping unchanged parts.
