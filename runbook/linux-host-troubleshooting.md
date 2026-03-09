Get admin privileges 

* sudo -H -i -u lvadmin
---


To check the Average CPU Time of a Process

* ps -eo "%p %y %x %C %c" --sort c

.For thread count use:

ps uH p <PID_OF_U_PROCESS> | wc -l

---
  The following command will show the list of top processes ordered by RAM and CPU use in descendant form (remove the pipeline and head if you want to see the full list):
  
  * ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
 ----
https://curl.se/docs/manpage.html

* curl -d 'clientid=3171034&cip=0' http://host.domain.net:8080/queuer_17.0//acct-setcip
  
curl -d, --data <data>

(HTTP MQTT) Send the specified data in a POST request to the HTTP server, in the same way that a browser does when a user has filled in an HTML form and presses the submit button. This option makes curl pass the data to the server using the content-type application/x-www-form-urlencoded. 

*  wget -vX POST http://wrapper.livevox.com/wso2/services/owtrta/card/payment

  
----
 uptime
 
[rpargaonkar@acd121 ~]$ ps -p 30168  -o lstart
                 STARTED
Tue Jan 14 04:12:00 2020

Get the count of files from all directory and sub directory => use it mount switch. 

* find /mnt/lvpclient/ -type f -print | wc -ll

To get ftp service uptime, use the following command:

* [rpargaonkar@ftpin100.ny1 ~]$ ps -p $(ps -aef | grep proftpd | tail -1 | awk '{print $2}') -o etime

cat /proc/locks

cat /proc/loadavg

nproc

--------------------------------------------------------------
sar -q | more

12:00:01 AM   runq-sz  plist-sz   ldavg-1   ldavg-5  ldavg-15


07:50:01 AM         1       268      1.69      1.42      0.96
08:00:01 AM         1       319      2.05      1.81      1.34
08:10:01 AM         1     24750      1.96      2.06      1.70
08:20:01 AM         4     31537      1.60      1.75      1.71
08:30:01 AM         6     31541      2.43      2.70      2.22
08:40:01 AM         2       510    250.58   1657.72    981.15
08:50:01 AM         0       490      0.64    223.04    514.52
09:00:02 AM         1       497      0.62     30.47    269.90
09:10:01 AM         0       493      0.50      4.53    141.67
09:20:01 AM         0       496      0.50      1.01     74.44

 runq-sz          Run queue length (number of tasks waiting for run time).

 plist-sz         Number of tasks in the task list.

 ldavg-1        System load average for the last minute.  The load average is  calculated  as
                the  average number of runnable or running tasks (R state), and the number of
                tasks in uninterruptible sleep (D state) over the specified interval.

 ldavg-5        System load average for the past 5 minutes.

 ldavg-15       System load average for the past 15 minutes.
----------------------------------------------------------------
To get service uptime or restart hour
For hosts that are running Java 

 * ps -p "$(pidof java)" -o lstart
	
For Media Servers

* ps -p "$(pidof SrvMain)" -o lstart
	
It can also be replaced with a pid if we do not know the command that initiates the process

 ps -p "20615" -o lstart
 -----------
[rpargaonkar@job102.na4.or1 ~]$ ps -p 2577
  PID TTY          TIME CMD
 2577 ?        11:48:05 java

sudo -H -i -u lvadmin
[rpargaonkar@job102.na4.or1 ~]$ ps -p 24353 -o comm=
java

--check for port 1521
 netstat -an | grep 1521

--to checkt the thread count
cat /proc/3208/status
ps -p "$(pidof java)" -o lstart
00000000000000000000--------------------000000000000-------------
dmerchan@tma1103 ~]$ sudo /usr/local/lv/sbc_6.0/service.sh exec cli "show calls count"

31 total.

0000000000000000000000000000-----------------000000000

grep -i concurrency /usr/local/lv/tomcat_8300/webapps/inputfilter_3.0.0/WEB-INF/classes/application.properties

0000000000000000000-------------------0000000000
 sudo -H -i -u lvadmin

sed -n '/16:34:45/ , /16:35:59/p' job-scheduler.log.2016-03-28-20 | grep 19195


sed -n '/16:43:18/ , /16:59:59/p' WebServiceAPI.2019-03-28-08.log | grep JAXRSUtils
MRG_AuthBlast20151102.txt
sed -n '/05:42:30/ , /05:42:44/p' WebServiceAPI.2019-03-28-08.log | grep JAXRSUtils
sed -n '/21:48:00/ , /23:22:00/p' 06:07:00 06:16:34

[rpargaonkar@log101 prd]$ sed -n '/14:00:00/ , /14:15:59/p' acd126.ny1.livevox.net/VirtualACD_10.0.126/app.log.2019-09-03-09 acd126.ny1.livevox.net/VirtualACD_10.0.126/conference.log.2019-09-03-09 | grep '102935795117\|RSLAGLE' | more

grep -src 'ORA-01403' /mnt/app_logs/prd/rec101*/recording_13.0/app-2022-09-11* | cut -d "/" -f 5-8 | sort -r -n

grep -i 'failed\|error' lvp123.na4.or1.livevox.net/lvp_12.0/app.log.2020-01-27-01

grep -E -lr '467367670|3182305484' /mnt/ftpuploads/Conns-Coll/dnc/done/* | xargs ls -lrth
 grep -A 15 'Failed to Import Contact, Client Id: 59048'  contact100.ny1.livevox.net/contact_10.0_8000/app.log.2020-02-09-* | grep -v INFO | less

cat /usr/local/lv/DSI_12.0/release/na5/logback.groovy
...
-----------

find /export/livevox_logs/pdas10/logs -type f -mmin -5 -exec zgrep "updateContactDnd call complete. dur=9\|updateContactDnd call complete. dur=1\|updateContactDnd call complete. dur=8\|updateContactDnd call complete. dur=7\|updateContactDnd call complete. dur=6\|updateContactDnd call complete. dur=5\|updateContactDnd call complete. dur=4\|updateContactDnd call complete. dur=3\|updateContactDnd call complete. dur=2" {} \;
--
my bashrc
cd /var/livevox_logs/
alias ll="ls -lta | more"
alias ps="ps -ef | grep java"

tail -n 20 /var/livevox_logs/11.0_dsi126_8100/app.log
cat /usr/local/lv/tomcat_8100/webapps/DSI_11.0/WEB-INF/tomcat.properties
ps -ef | grep java


 grep -C 5 723451 app.log.2020-05-18-14 | less
 
 Grep Special Characters
 grep "[]:/?#@\!\$&'()*+,;=%[]"
--------Must Learn---------
using vmstat

Interpreting VMSTAT

Diagnose Sluggish Server using Uptime and TOP

Interpreting top command output in detail

diagnose CPU High user time and high memory usage issues

trouble shooting high load after the fact-sar utility

diagnosing high I/O using IOSTAT 

Interpreting historical data collected by SAR utility for performance issues
