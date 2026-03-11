# Linux Log Investigation Commands (Used in Production servers formatted using chatgpt)

## 1. Extract logs between two timestamps and filter by ID

```bash
sed -n '/16:34:45/ , /16:35:59/p' job-scheduler.log.2016-03-28-20 | grep 19195
```

### Purpose

Extract log entries between **two timestamps** and filter lines containing a **specific job ID**.

### Breakdown

**sed**

* `-n` → Suppress automatic printing of lines
* `/start/ , /end/` → Select range between two matching patterns
* `p` → Print the selected lines

**grep**

* `19195` → Filter lines containing job ID `19195`

### Use Case

Investigate **job scheduler activity** for a specific job within a time window.

---

# 2. Extract logs in time range and filter by component

```bash
sed -n '/16:43:18/ , /16:59:59/p' WebServiceAPI.2019-03-28-08.log | grep JAXRSUtils
```

### Purpose

Find logs related to **JAXRSUtils component** within a specific time window.

### Breakdown

**sed**

* Select log entries between **16:43:18 and 16:59:59**

**grep**

* Filters logs mentioning **JAXRSUtils** ( related to REST API processing).

### Use Case

Debug **REST API request handling issues**.

---

# 3. Extract logs across multiple files and filter multiple patterns

```bash
sed -n '/14:00:00/ , /14:15:59/p' acd126.ny1.livevox.net/VirtualACD_10.0.126/app.log.2019-09-03-09 acd126.ny1.livevox.net/VirtualACD_10.0.126/conference.log.2019-09-03-09 | grep '102935795117\|RSLAGLE' | more
```

### Purpose

Search multiple log files for specific **call IDs or agent IDs** within a time range.

### Breakdown

**sed**

* Extract logs between **14:00 and 14:15**
* Works on **multiple log files simultaneously**

**grep**

* `'pattern1\|pattern2'` → OR condition
* Searches for:

  * `102935795117` (likely call/session ID)
  * `RSLAGLE` (agent/login ID)

**more**

* Displays output **page-by-page**

### Use Case

Investigating **call routing or agent session activity**.

---

# 4. Search logs recursively for Oracle error and extract relevant path

```bash
grep -src 'ORA-01403' /mnt/app_logs/prd/rec101*/recording_13.0/app-2022-09-11* | cut -d "/" -f 5-8 | sort -r -n
```

### Purpose

Find occurrences of **Oracle error ORA-01403** across multiple log directories and summarize affected components.

### Breakdown

**grep**

* `-s` → Suppress error messages
* `-r` → Search recursively in directories
* `-c` → Count occurrences per file

**cut**

* `-d "/"` → Use `/` as field delimiter
* `-f 5-8` → Extract fields 5–8 from file path

**sort**

* `-r` → Reverse order
* `-n` → Numeric sorting

### Use Case

Identify **which components generate the most database errors**.

---

# 5. Case-insensitive search for failures and errors

```bash
grep -i 'failed\|error' lvp123.na4.or1.livevox.net/lvp_12.0/app.log.2020-01-27-01
```

### Purpose

Search log file for **any failure or error messages**.

### Breakdown

**grep**

* `-i` → Case insensitive search
* `'failed\|error'` → Match either `failed` or `error`

### Use Case

Quick scan for **application failures during incidents**.

---

# 6. Find files containing specific account/phone numbers

```bash
grep -E -lr '467367670|3182305484' /mnt/ftpuploads/Conns-Coll/dnc/done/* | xargs ls -lrth
```

### Purpose

Find files containing specific **phone numbers or identifiers** and list file details.

### Breakdown

**grep**

* `-E` → Extended regex
* `-l` → Show filenames only
* `-r` → Recursive search
* `'467367670|3182305484'` → Match either number

**xargs**

* Pass file list to another command

**ls**

* `-l` → Detailed listing
* `-r` → Reverse order
* `-t` → Sort by modification time
* `-h` → Human readable file sizes

### Use Case

Trace **DNC upload files or customer records**.

---

# 7. Show context around an error and remove noise

```bash
grep -A 15 'Failed to Import Contact, Client Id: 59048' contact100.ny1.livevox.net/contact_10.0_8000/app.log.2020-02-09-* | grep -v INFO | less
```

### Purpose

Investigate **contact import failure** and display surrounding log context.

### Breakdown

**grep**

* `-A 15` → Show 15 lines **after the matching line**

**second grep**

* `-v INFO` → Exclude lines containing `INFO` (remove noise)

**less**

* Scrollable log viewer

### Use Case

Debug **data import failures while ignoring normal informational logs**.

---

# Common Tools Used in These Pipelines

| Command       | Purpose                                     |
| ------------- | ------------------------------------------- |
| `sed`         | Stream editor used to extract log ranges    |
| `grep`        | Pattern search in files                     |
| `cut`         | Extract specific fields                     |
| `sort`        | Sort output                                 |
| `xargs`       | Pass output as arguments to another command |
| `more / less` | View output interactively                   |

---

# Advanced Log Analysis

## Search compressed logs modified in last 5 minutes

```bash
find /export/livevox_logs/pdas10/logs -type f -mmin -5 -exec zgrep "updateContactDnd call complete" {} \;
```

**Explanation**

| Option     | Meaning                          |
| ---------- | -------------------------------- |
| `-mmin -5` | Files modified in last 5 minutes |
| `-exec`    | Execute command on each file     |
| `zgrep`    | Search inside compressed logs    |

---

## Search logs with context

```bash
grep -C 5 723451 app.log.2020-05-18-14 | less
```

**Explanation**

| Option | Meaning                             |
| ------ | ----------------------------------- |
| `-C 5` | Show 5 lines before and after match |
| `less` | Scrollable viewer                   |

---

## Search special characters in logs

```bash
grep "[]:/?#@\!\$&'()*+,;=%[]"
```

Used when logs contain **special characters or encoded URLs**.

---

# 12. Useful Shell Aliases

Example `.bashrc` shortcuts:

```bash
cd /var/livevox_logs/

alias ll="ls -lta | more"

alias ps="ps -ef | grep java"
```

---

# 13. Quick Log & Service Checks

### View last 20 lines of log

```bash
tail -n 20 /var/livevox_logs/11.0_dsi126_8100/app.log
```

