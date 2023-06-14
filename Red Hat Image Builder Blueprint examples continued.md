
```

name = "fedora"
description = "Fedora IMage"
distro = "fedora-37"

[customizations.kernel]
append = "net.ifnames.prefix=net quiet systemd.show_status=yes"

# Filesystem
#
[[customizations.filesystem]]
mountpoint = "/boot"
size = "1 GiB"
#[[customizations.filesystem]]
#mountpoint = "swap"
#size = "2 GiB"
[[customizations.filesystem]]
mountpoint = "/"
size = "8 GiB"
[[customizations.filesystem]]
mountpoint = "/home"
size = "2 GiB"
[[customizations.filesystem]]
mountpoint = "/tmp"
size = "2 GiB"
[[customizations.filesystem]]
mountpoint = "/var"
size = "8 GiB"
[[customizations.filesystem]]
mountpoint = "/var/log"
size = "2 GiB"
[[customizations.filesystem]]
mountpoint = "/var/log/audit"
size = "2 GiB"
[[customizations.filesystem]]
mountpoint = "/var/tmp"
size = "2 GiB"

# Install packages. Each individual package needs a block
[[packages]]
name = "nginx"
version = "*"

[[packages]]
name = "ansible"
version = "*"

[[packages]]
name = "postgresql"
version = "*"



[customizations]
hostname = "HOSTNAME"

# Set ssh key for existing users
[[customizations.sshkey]]
user = "root"
key = "" 

# Set timezone
[customizations.timezone]
timezone = "Europe/London"
ntpservers = ["pool 2.fedora.pool.ntp.org iburst"]

# Set locale
[customizations.locale]
languages = ["en_UK.UTF-8"]
keyboard = "uk"

# Create a new user
# Replace PASSWORD-HASH with the actual password hash. To generate the hash, use a command such as:
# python3 -c 'import crypt,getpass;pw=getpass.getpass();print(crypt.crypt(pw) if (pw==getpass.getpass("Confirm: ")) else exit())'
# Replace PUBLIC-SSH-KEY with the actual public key
# Only the user name is required - you can leave out anything else
# Repeat this block for every user to be created
[[customizations.user]]
name = "obi"
description = "USER-DESCRIPTION"
password = ""
key = ""
home = "/home/obi/"
shell = "/usr/bin/bash"
groups = ["users", "wheel"]
uid = 1000
gid = 1000

# Give user sudo access
[[customizations.sudo]]
name = "obi"
nopasswd = false
commands = ["ALL"]

# Create a new group. The name is required but GID is optional
# Repeat this block for every group to be created
[[customizations.group]]
name = "GROUP-NAME"
gid = 1000

# Configure firewall ports
[customizations.firewall]
port = ["80/tcp", "443/tcp", "22/tcp"]


# Configure firewall services
[customizations.firewall.services]
enabled = ["http", "https"]
#disabled = ["http", "https"]

# Configure services
[customizations.services]
enabled = ["nginx"]
#disabled = ["nginx", "postgresql"]


# Edits files that live under /etc - The bash script lives the same folder as the blueprint file
[[customizations.script]]
name = "edit_files.sh"

# creates files in the /var dir - The bash script lives the same folder as the blueprint file
[[customizations.script]]

name = "create_test.sh"


```

## edit_files.sh
```bash
#!/bin/bash
# Edit the /etc/motd file

echo "Welcome to my custom image!" > /etc/motd
```

## create_test.sh

```bash
#!/bin/bash  

# Edit the /etc/motd file

touch /var/test.txt


```
