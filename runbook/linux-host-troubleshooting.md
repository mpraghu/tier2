# Linux System Diagnostics & Troubleshooting Commands

This document contains commonly used Linux commands for **system diagnostics, log analysis, and service troubleshooting** in production environments.

---

# 1. Privilege Escalation

### Switch to Admin User

```bash
sudo -H -i -u lvadmin
```
| Option       | Meaning                            |
| ------------ | ---------------------------------- |
| `sudo`       | Execute command as another user    |
| `-H`         | Sets HOME directory to target user |
| `-i`         | Start login shell                  |
| `-u lvadmin` | Switch to `lvadmin` user           |

**Use case**

Used when administrative access is required for **LiveVox application management or troubleshooting**.

---

# 2. Process Monitoring

## View CPU usage by process

```bash
ps -eo "%p %y %x %C %c" --sort c
```

**Explanation**

| Option     | Meaning                |
| ---------- | ---------------------- |
| `ps`       | Process status command |
| `-e`       | Show all processes     |
| `-o`       | Custom output format   |
| `%p`       | Process ID             |
| `%y`       | TTY                    |
| `%x`       | CPU time               |
| `%C`       | CPU usage              |
| `%c`       | Command name           |
| `--sort c` | Sort by CPU usage      |

---

## Show top memory and CPU consuming processes

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
```

**Explanation**

| Option         | Meaning                      |
| -------------- | ---------------------------- |
| `%mem`         | Memory usage percentage      |
| `%cpu`         | CPU usage                    |
| `--sort=-%mem` | Sort by highest memory usage |
| `head`         | Show first 10 lines          |

**Use case**

Quickly identify **top resource-consuming processes**.

---

## Count threads of a process

```bash
ps uH p <PID> | wc -l
```

**Explanation**

| Command   | Meaning                    |
| --------- | -------------------------- |
| `ps uH`   | Display process threads    |
| `p <PID>` | Filter by process ID       |
| `wc -l`   | Count lines (thread count) |

**Use case**

Useful for **Java thread leak investigations**.

---

# 3. Service Uptime & Process Start Time

## Get Java service start time

```bash
ps -p "$(pidof java)" -o lstart
```

**Explanation**

| Option       | Meaning                    |
| ------------ | -------------------------- |
| `pidof java` | Find Java process PID      |
| `-p`         | Specify PID                |
| `-o lstart`  | Display process start time |

---

## Media Server process uptime

```bash
ps -p "$(pidof SrvMain)" -o lstart
```

---

## Using a specific PID

```bash
ps -p 20615 -o lstart
```

---

## FTP service uptime

```bash
ps -p $(ps -aef | grep proftpd | tail -1 | awk '{print $2}') -o etime
```

**Explanation**

| Command            | Meaning              |
| ------------------ | -------------------- |
| `ps -aef`          | List all processes   |
| `grep proftpd`     | Filter FTP process   |
| `awk '{print $2}'` | Extract PID          |
| `etime`            | Process elapsed time |

---

# 4. Network & Port Diagnostics

## Check if Oracle DB port is listening

```bash
netstat -an | grep 1521
```

**Explanation**

| Option        | Meaning                 |
| ------------- | ----------------------- |
| `netstat -an` | Show active connections |
| `grep 1521`   | Filter Oracle DB port   |

---

# 5. HTTP / API Testing

## Send HTTP POST request using curl

```bash
curl -d 'clientid=3171034&cip=0' http://host.domain.net:8080/queuer_17.0//acct-setcip
```

**Explanation**

| Option                              | Meaning                |
| ----------------------------------- | ---------------------- |
| `-d`                                | Send POST request data |
| `application/x-www-form-urlencoded` | Form data format       |

Equivalent to submitting an **HTML form request**.

---

## POST request using wget

```bash
wget -vX POST http://wrapper.livevox.com/wso2/services/owtrta/card/payment
```

**Explanation**

| Option    | Meaning              |
| --------- | -------------------- |
| `-v`      | Verbose output       |
| `-X POST` | Use HTTP POST method |

---

# 6. File System Operations

## Count files recursively

```bash
find /mnt/lvpclient/ -type f -print | wc -l
```

**Explanation**

| Option    | Meaning           |
| --------- | ----------------- |
| `find`    | Search filesystem |
| `-type f` | Files only        |
| `wc -l`   | Count files       |

---

# 7. System Resource Monitoring

## CPU count

```bash
nproc
```

Returns number of **CPU cores available**.

---

## System load averages

```bash
cat /proc/loadavg
```

Displays:

```
1-minute load
5-minute load
15-minute load
```

---

## Check file locks

```bash
cat /proc/locks
```

Shows **active file locks**.

---

# 8. System Performance Analysis

## Historical system load analysis

```bash
sar -q | more
```

### Key metrics

| Field    | Meaning               |
| -------- | --------------------- |
| runq-sz  | Run queue length      |
| plist-sz | Total processes       |
| ldavg-1  | Load average (1 min)  |
| ldavg-5  | Load average (5 min)  |
| ldavg-15 | Load average (15 min) |

---

# 9. SBC / Telephony Diagnostics

## Check active calls in SBC

```bash
sudo /usr/local/lv/sbc_6.0/service.sh exec cli "show calls count"
```

**Purpose**

Execute CLI command inside the **Session Border Controller (SBC)**.

Displays **current active call count**.

Example output:

```
31 total
```

**Use case**

Verify abnormal **call volume spikes or traffic issues**.

---

# 10. Application Configuration Checks

## Check concurrency configuration

```bash
grep -i concurrency /usr/local/lv/tomcat_8300/webapps/inputfilter_3.0.0/WEB-INF/classes/application.properties
```

**Use case**

Verify **thread/concurrency limits** in InputFilter service.

---


---

### Check Tomcat configuration

```bash
cat /usr/local/lv/tomcat_8100/webapps/DSI_11.0/WEB-INF/tomcat.properties
```

---

### Check Java processes

```bash
ps -ef | grep java
```

---

# 14. Key Performance Troubleshooting Tools

These commands should be mastered for production troubleshooting.

| Tool     | Purpose                             |
| -------- | ----------------------------------- |
| `vmstat` | Memory, CPU, and process statistics |
| `top`    | Real-time system monitoring         |
| `iostat` | Disk I/O diagnostics                |
| `sar`    | Historical performance analysis     |
| `uptime` | System load summary                 |

---

# 15. Common Troubleshooting Scenarios

| Issue               | Tools                 |
| ------------------- | --------------------- |
| High CPU            | `top`, `ps`, `vmstat` |
| High memory         | `top`, `ps`, `free`   |
| High disk I/O       | `iostat`              |
| High load           | `uptime`, `sar -q`    |
| Application failure | `grep`, `sed`, `tail` |

---


