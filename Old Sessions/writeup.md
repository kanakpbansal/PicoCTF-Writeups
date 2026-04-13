# <div align="center">[Old Sessions](https://play.picoctf.org/practice/challenge/739?category=1&difficulty=1&page=1)</div>
<div align="center">Web Exploitation</div>
<br>


# Challenge
Proper session timeout controls are critical for securing user accounts. If a user logs in on a public or shared computer but doesn’t explicitly log out (instead simply closing the browser tab), and session expiration dates are misconfigured, the session may remain active indefinitely.

This then allows an attacker using the same browser later to access the user’s account without needing credentials, exploiting the fact that sessions never expire and remain authenticated.

Your friend tells you to check out a new social media platform he built a few years ago. Although its still under development, he said the site is almost complete. He also mentioned that he hates constantly logging into sites, and so has made his page that 'once you login, you never have to log-out again'!
Browse here, and find the flag!

<br>

> Flag

When visiting the website, I was presented with a login page that also included a registration option. After registering and logging in successfully, I gained access to a simple social media interface where multiple users had posted messages.

While exploring the platform, I noticed a few suspicious clues:

1. One of the user: mary_jones_8992 tweeted this `Hey I found a strange page at /sessions`
2. A user named Admin had also posted a basic "Hello World" message, suggesting testing activity

Going to /sessions I came across the following:
```
1) session:JedzGdDbmX-CCTJbesI0FI_1c5WgZZ5QXSxwsKfhwRE, {'_permanent': True, 'key': 'admin'}

2) session:YKljph9MSYjY1nDiHRTtZDmTpJgpmY32luiF4k1_Yc4, {'_permanent': True, 'key': 'myusername'}
```
(Here, myusername corresponds to the account I created)

From this, I deduced that:

- These values represent active session IDs
- Each session is tied to a specific user via the 'key' field
- Sessions are marked as _permanent: True, meaning they do not expire

To verify this, I opened the browser’s developer tools and navigated to: `Application → Cookies`

I observed that my current session ID matched the second session listed (myusername).
This confirmed that authentication was entirely dependent on the session cookie.

Since the application does not validate session ownership properly and allows sessions to persist indefinitely, I attempted a session hijacking attack:
- Copied the session ID associated with the admin user
- Replaced my own session cookie value with the admin’s session ID
- Reloaded the page

As a result, I was logged in as the admin user and successfully retrieved the flag.

Answer : 

```
picoCTF{s3t_s3ss10n_3xp1rat10n5_77b6684a}
```


<br>

# 🧠 Summary
- Sessions should never be publicly exposed (like /sessions)
- Session IDs must be kept secret and securely stored
- Proper session expiration/timeout is essential
- Applications should validate session ownership, not just trust the cookie
- Use secure practices like HttpOnly, Secure flags, and server-side checks to prevent hijacking

<br>
