\# Day 3: Users and Permissions



\## What I did

\- Looked at users with `whoami`, `id` and `/etc/passwd`

\- Created a test user (`tester`) with `sudo adduser`

\- Practised file permissions with `chmod` and ownership with `chown`

\- Used `sudo -u tester` to test access as a different user



\## Key concepts



\*\*Reading `/etc/passwd`:\*\*

`username:x:UID:GID:description:home:shell`

\- root has UID 0

\- Service accounts use `/usr/sbin/nologin` so nobody can log in as them



\*\*Reading permissions (`ls -l`):\*\*

`-rw-r--r--` = owner / group / others

\- r = read (4), w = write (2), x = execute (1)

\- 600 = owner read/write only

\- 644 = owner read/write, everyone else read only

\- 700 = owner full access, nobody else (used for folders)



\## Commands learned

| Command | What it does |

|---|---|

| `adduser name` | creates a user |

| `id name` | shows a user's ID and groups |

| `chmod 600 file` | sets permissions |

| `chown user:group file` | changes the owner |

| `ls -l` / `ls -ld` | shows permissions of files / folders |

| `sudo -u user command` | runs a command as another user |



\## Experiments



\*\*1. File permissions test\*\*

\- Set `/tmp/secret.txt` to 600, then `tester` ran `cat` on it: \*\*Permission denied\*\*

\- Set it to 644, then `tester` ran `cat` on it: \*\*it worked\*\*

\- Used `chown` to change the file's owner to `tester`



\*\*2. Folder permissions test\*\*

\- Created `/tmp/vault` and put a file in it

\- With the folder open, `tester` could read the file

\- After `chmod 700 /tmp/vault`, `tester` got \*\*Permission denied\*\*, even though the file itself was still readable

\- \*\*Lesson:\*\* folder permissions control access to everything inside it



\## Mistakes and fixes

\- Typed `/tmp/secret/txt` instead of `/tmp/secret.txt`, so I got "No such file". Fix: check the path carefully.

\- Used `/vault/...` instead of `\~/vault/...`. `/` is the system root, while `\~` is my home folder.

\- Ran `chmod` on a file when the task needed it on the folder.



\## Security takeaways

\- \*\*Least privilege:\*\* give users only the access they need

\- \*\*SSH private keys must be 600.\*\* If other users could read them, they could impersonate me.

\- \*\*`/etc/shadow` stores password hashes\*\* and is restricted to root and a system group. If it were world-readable, anyone on the system could copy the hashes and try to crack them offline.

\- Wrong permissions are a common real-world misconfiguration that attackers look for.





