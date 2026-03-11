Sections:

```
1. Finding most frequent errors
2. Detecting abusive IP traffic
3. Finding slow API calls
4. Traffic spike detection
5. Transaction tracing across services
```
# 1️⃣ Find the most frequent errors in a log

```bash
grep -i error app.log | awk -F':' '{print $NF}' | sort | uniq -c | sort -nr | head
```

### What it does

Shows **top recurring error messages**.

### Breakdown

| Command                   | Purpose                  |
| ------------------------- | ------------------------ |
| `grep -i error`           | find error lines         |
| `awk -F':' '{print $NF}'` | extract error message    |
| `sort`                    | group similar messages   |
| `uniq -c`                 | count occurrences        |
| `sort -nr`                | show highest count first |
| `head`                    | top 10 errors            |

### Output example

```
154 Database connection failed
87 Timeout while calling API
22 NullPointerException
```

# 2️⃣ Find top IPs hitting a server

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

### What it does

Shows **top client IPs hitting a web server**.

### Breakdown

| Part       | Meaning                  |
| ---------- | ------------------------ |
| `$1`       | first field (IP address) |
| `uniq -c`  | count occurrences        |
| `sort -nr` | show highest first       |

### Output example

```
20451 192.168.10.15
18022 10.23.4.1
9012 52.88.120.3
```

### To Detect:

* traffic spikes
* abusive clients
* DDoS sources

---

# 3️⃣ Find slow API calls from logs

Example log:

```
API completed in 345 ms
```

Command:

```bash
grep "completed in" app.log | awk '{print $(NF-1)}' | sort -nr | head
```

### What it does

Shows **slowest API calls**.

### Breakdown

| Command       | Purpose                 |
| ------------- | ----------------------- |
| `grep`        | find response time logs |
| `awk $(NF-1)` | extract response time   |
| `sort -nr`    | highest latency first   |

### Example output

```
9876
8542
7011
```

### Why it's powerful

Quickly identifies:

> **Which requests are slowest in production**

---

# 4️⃣ Count requests per minute (traffic spike detection)

```bash
awk '{print substr($4,2,17)}' access.log | sort | uniq -c | sort -nr | head
```

### What it does

Shows **request volume per minute**.

### Breakdown

| Part              | Meaning               |
| ----------------- | --------------------- |
| `substr($4,2,17)` | extract timestamp     |
| `uniq -c`         | count requests        |
| `sort -nr`        | highest traffic first |

### Example output

```
4521 10/Mar/2026:14:32
4102 10/Mar/2026:14:33
3901 10/Mar/2026:14:31
```

### To Detect:

* traffic spikes
* sudden bursts
* DDoS attacks

---

# 5️⃣ Trace a request across logs (transaction tracing)

```bash
grep -R "transactionId=847239" /var/log/ | sort
```

### What it does

Searches **all logs for a transaction ID**.

### Breakdown

| Option     | Meaning             |
| ---------- | ------------------- |
| `-R`       | recursive search    |
| `/var/log` | search across logs  |
| `sort`     | chronological order |

### Example output

```
API request received
DB query started
DB query completed
API response sent
```

### Why it's powerful

Used for **distributed system debugging**.

Example scenario:

```
API -> Queue -> Worker -> Database
```

You trace the **same transaction ID across services**.

---

Find **top error-producing services**.

```bash
grep -i error *.log | awk -F'/' '{print $NF}' | sort | uniq -c | sort -nr
```

Output:

```
120 api.log
87 scheduler.log
21 worker.log
```

Will help us to instantly know -> **Which service is failing most.**

---
