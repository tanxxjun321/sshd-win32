# install sshd on msys2.
1. install packages.
``` shell
pacman -S --noconfirm mingw-w64-x86_64-editrights
pacman -S --noconfirm openssh
pacman -S --noconfirm cygrunsrv
```

2. set passwd.
``` shell
mkpasswd -l > /etc/passwd
mkgroup  -l > /etc/group

passwd <username> #Enter a password here.
```

3. generate ssh key.
``` shell
ssh-keygen -A
ssh-keygen -b 4096
```

4. configure sshd.
- Put `AcceptEnv MSYSTEM` into `/etc/ssh/sshd_config` on the remote machine.
- Put `SendEnv   MSYSTEM` into `/etc/ssh/ssh_config` or `~/.ssh/config` on the local machine.

# stop / start sshd
``` shell
net stop  sshd
net start sshd
```

# uninstall sshd

- cmd or powershell:
``` shell
net user /del sshd
net user /del sshd_server
```
- bash
``` shell
cygrunsrv -R sshd
cygrunsrv -R sshd_server
```
- remove line:`/etc/passwd` contains sshd or sshd_server.
