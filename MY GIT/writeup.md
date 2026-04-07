# <div align="center">[MY GIT](https://play.picoctf.org/practice/challenge/764?originalEvent=79&page=1)</div>
<div align="center">General CLI skills</div>
<br>


# Challenge
I have built my own Git server with my own rules!
You can clone the challenge repo using the command below.
git clone ssh://git@foggy-cliff.picoctf.net:62626/git/challenge.git
Here's the password: 921cd55c
Check the README to get your flag!

> Flag

After typing the given command in my CLI i got the following output: 
```
Cloning into 'challenge'...
The authenticity of host '[foggy-cliff.picoctf.net]:62626 ([3.15.249.208]:62626)' can't be established.
ED25519 key fingerprint is: SHA256:Grm7IvZgdCDbXv3DtQ70/6WKHA2q3XhT+sfva8nLT38
This host key is known by the following other names/addresses:
    ~/.ssh/known_hosts:21: [hashed name]
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[foggy-cliff.picoctf.net]:62626' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
git@foggy-cliff.picoctf.net's password:
```
The password provided is : `921cd55c`

Output:
```
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
```

This github repo was cloned into a folder named `challenge` which had a `README.md` file with the following content: 

```
# MyGit

### If you want the flag, make sure to push the flag!

Only flag.txt pushed by ```root:root@picoctf``` will be updated with the flag.

GOOD LUCK!
```
This meant that if my username and email are `root:root@picoctf` and I push a flag.txt with any content the server will replace it with the actual flag

So I configured my username and email as reuired using the following commands :
- Username: `git config user.name "root"`
- Email: `git config user.email "root@picoctf"`

I created a pseudo flag.txt:
`echo "give me flag" > flag.txt`

And pushed it to githib using the usual commands : `git add flag.txt` followed by `git commit -m "Flag"` I checked the branch using `git branch` 

Output: `* master`

So I pushed the flag onto the master branch with: `git push origin master`

The server responded with:
```
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
git@foggy-cliff.picoctf.net's password: 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 272 bytes | 272.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Author matched and flag.txt found in commit...
remote: Congratulations! You have successfully impersonated the root user
remote: Here's your flag: picoCTF{1mp3rs0n4t4_g17_345y_cd8540cd}
To ssh://foggy-cliff.picoctf.net:62626/git/challenge.git
   aa44ed9..ce0e04d  master -> master
```

Answer : 

```
picoCTF{1mp3rs0n4t4_g17_345y_cd8540cd}
```


<br>

# 🧠 Summary
- Cloned the challenge Git repository using provided SSH credentials
- Analyzed README.md to understand the server’s condition
- Identified that the server trusts Git author metadata
- Spoofed identity by setting user.name and user.email to root@picoctf
- Created and committed a file named flag.txt
- Pushed the commit to the remote repository
- Server validated conditions and revealed the flag during push
- Exploited Git identity spoofing vulnerability to obtain the flag

<br>
