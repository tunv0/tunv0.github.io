---
hide:
  - toc        # Hide table of contents
---

# <a href='https://github.com/Tib3rius/AutoRecon' target="blank">AutoRecon</a>

``` bash
┌──(Hades㉿10.10.14.149)-[0.7:15.4]~/autoscan/AutoRecon/src/autorecon
└─$ python3 autorecon.py 10.10.10.207
[*] Scanning target 10.10.10.207
/home/kali/autoscan/AutoRecon/src/autorecon/autorecon.py:503: DeprecationWarning: The explicit passing of coroutine objects to asyncio.wait() is deprecated since Python 3.8, and scheduled for removal in Python 3.11.
  done, pending = await asyncio.wait(pending, return_when=FIRST_COMPLETED)
[*] Running service detection nmap-top-20-udp on 10.10.10.207
[*] Running service detection nmap-quick on 10.10.10.207
[*] Running service detection nmap-full-tcp on 10.10.10.207
[!] Service detection nmap-top-20-udp on 10.10.10.207 returned non-zero exit code: 1
[*] Service detection nmap-quick on 10.10.10.207 finished successfully in 40 seconds
[*] Found ssh on tcp/22 on target 10.10.10.207
[*] Found http on tcp/80 on target 10.10.10.207
[*] Running task tcp/22/sslscan on 10.10.10.207
[*] Running task tcp/22/nmap-ssh on 10.10.10.207
[*] Running task tcp/80/sslscan on 10.10.10.207
[*] Running task tcp/80/nmap-http on 10.10.10.207
[*] Running task tcp/80/curl-index on 10.10.10.207
[*] Running task tcp/80/curl-robots on 10.10.10.207
[*] Running task tcp/80/wkhtmltoimage on 10.10.10.207
[*] Running task tcp/80/whatweb on 10.10.10.207
[*] Running task tcp/80/nikto on 10.10.10.207
/home/kali/autoscan/AutoRecon/src/autorecon/autorecon.py:281: DeprecationWarning: The explicit passing of coroutine objects to asyncio.wait() is deprecated since Python 3.8, and scheduled for removal in Python 3.11.
  await asyncio.wait([
[*] Task tcp/22/sslscan on 10.10.10.207 finished successfully in less than a second
[*] Task tcp/80/sslscan on 10.10.10.207 finished successfully in less than a second
[*] Running task tcp/80/gobuster on 10.10.10.207
[*] Task tcp/80/curl-robots on 10.10.10.207 finished successfully in 1 second
[*] Task tcp/80/curl-index on 10.10.10.207 finished successfully in 1 second
[*] Task tcp/80/wkhtmltoimage on 10.10.10.207 finished successfully in 5 seconds
[*] Task tcp/22/nmap-ssh on 10.10.10.207 finished successfully in 11 seconds
[*] [12:44:03] - There are 5 tasks still running on 10.10.10.207
[*] Task tcp/80/whatweb on 10.10.10.207 finished successfully in 29 seconds
[*] [12:45:03] - There are 4 tasks still running on 10.10.10.207
[*] [12:46:03] - There are 4 tasks still running on 10.10.10.207
[*] Task tcp/80/nmap-http on 10.10.10.207 finished successfully in 2 minutes, 39 seconds
[*] [12:47:03] - There are 3 tasks still running on 10.10.10.207
[*] [12:48:03] - There are 3 tasks still running on 10.10.10.207
[*] Task tcp/80/gobuster on 10.10.10.207 finished successfully in 38 minutes, 59 seconds
[*] [13:23:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:24:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:25:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:26:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:27:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:28:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:29:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:30:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:31:05] - There are 2 tasks still running on 10.10.10.207
[*] [13:32:05] - There are 2 tasks still running on 10.10.10.207
[*] Task tcp/80/nikto on 10.10.10.207 finished successfully in 48 minutes, 39 seconds
[*] [13:33:05] - There is 1 task still running on 10.10.10.207
[*] [13:34:05] - There is 1 task still running on 10.10.10.207
[*] [13:35:05] - There is 1 task still running on 10.10.10.207
[*] [13:36:05] - There is 1 task still running on 10.10.10.207
[*] [13:37:05] - There is 1 task still running on 10.10.10.207
[*] [13:38:05] - There is 1 task still running on 10.10.10.207
[*] [13:39:05] - There is 1 task still running on 10.10.10.207
[*] [13:40:05] - There is 1 task still running on 10.10.10.207
[*] [13:41:05] - There is 1 task still running on 10.10.10.207
[*] [13:42:05] - There is 1 task still running on 10.10.10.207
[*] Service detection nmap-full-tcp on 10.10.10.207 finished successfully in 59 minutes, 42 seconds
[*] Finished scanning target 10.10.10.207 in 59 minutes, 42 seconds
[*] Finished scanning all targets in 59 minutes, 42 seconds!
```