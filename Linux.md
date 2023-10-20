# Scripting

Bash is unsuitable for anything that needs to work across various systems. It's not consistent from one system to another, nor is that one of its goals.

# Archives

extract a .tar.* archive

```
tar -xf archive.tar.gz -C path/to/directory
```

extract a .zip archive

```
unzip archive.zip -d path/to/directory
```

# SSH

## Daemon Config 

/etc/ssh/sshd_config
manpage: sshd_config

## Daemon Logs

/var/log/auth.log

## Generate a key

```shell
ssh-keygen -t ed25519 -C <email address>
```

## Start agent

How is this different from the daemon?

```shell
eval "$(ssh-agent -s)"
```

## "Add" a key

```shell
ssh-add ~/.ssh/id_ed25519
```

# SCP

Copy a directory

```shell
scp -r dir user@host:/path/name
```

# Systemd

Can be used (with `systemctl` command) to create and manage programs that run automatically on specific triggers, like when the system boots or with a timer.

Systemd service definitions can be found at `/etc/systemd/system/<service-name>.service`

Example: I'm using this to automatically configure static IP addresses

See the output of a service since a given time:
```shell
journalctl -S today -u web-monitor.service
```


# IP

You can find the default network interface with 

```shell
ip route list default
```
