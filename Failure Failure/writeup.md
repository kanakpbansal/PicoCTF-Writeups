# <div align="center">[Failure Failure](https://play.picoctf.org/practice/challenge/756?difficulty=2&originalEvent=79&page=1)</div>
<div align="center">Load balancer failover</div>
<br>


# Challenge
Welcome to Failure Failure — a high-available system.
This challenge simulates a real-world failover scenario where one server is prioritized over the other.
A load balancer stands between you and the truth — and it won't hand over the flag until you force its hand.
You can begin your journey here to try and retrieve the flag.
For reference:
The HAProxy configuration used in this challenge is available here.
The application code is available here

> Flag

After strating the instance I got three links:
1. The website
2. HAProxy configuration file
3. Application code

The website initially only said:
```
Welcome!!
No flag in this service
```
Nor was there any clue in the page source.
The Configuration file tells us how traffic is routed between servers. It gave the following information:
- HAProxy listens on port 80
- Sends traffic to backend servers
- Primary server (s1) handles all requests normally
- Backup server (s2) is used only if primary fails
- Health check every 2 seconds
- If primary fails 2 times (non-200 response) → marked DOWN
- Then traffic switches to backup

Most Important piece of information is revealed by the application code which says that the limit of the primary server is 300 per minute.

I used the following command to make simple curl requests to the primary server 500 times:
```
for i in {1..500}; do
  curl -s http://mysterious-sea.picoctf.net:51213/ > /dev/null &
done
wait
```

After running this command I reloaded the page, since the primary servers limit of 300 requests per min exceeded the backup server revealed the flag.

Answer : 

```
picoCTF{f41l0v3r_f0r_7h3_w1n_f8510432}
```


<br>

# 🧠 Summary
- Load balancer routes traffic to primary server by default
- Backup server is only used during failure
- Rate limiting causes primary to return 503 errors
- HAProxy detects failures via health checks
- After 2 failed checks → switches to backup
- Backup server reveals the flag

<br>
