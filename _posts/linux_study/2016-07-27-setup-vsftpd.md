---
layout: post
category: linux_study
title: Setup vsftpd on Ubuntu 14.10
date: 2016-07-27
---

# Setup vsftpd:

Install vsftpd:

```
sudo apt-get install vsftpd
```

Check if vsftpd installed successfully:

```
sudo service status vsftpd
```

Add `/home/uftp` as user home directory:

```
sudo mkdir /data/jinbin.lin/uftp
```

Add user `uftp` and set password:

```
sudo useradd -d /data/jinbin.lin/uftp -s /bin/bash uftp
```

Set user password (need to enter password twice):

```
sudo passwd uftp
```

Edit vsftpd configuration file:

```
/etc/vsftpd.conf
```

Add following commands at the end of `vsftpd.conf`:

```
userlist_deny=NO
userlist_enable=YES
userlist_file=/etc/allowed_users
```

Modify following configurations:

```
local_enable=YES
write_enable=YES
```

Edit `/etc/allowed_users`，add username: uftp

Check file `/etc/ftpusers`, delete `uftp` (if file contains this username). 
This file recording usernames which are forbidden to access FTP server.

Restart vsftpd:

```
sudo systemctl restart vsftpd
```

# Forbid user access top level directory:

Create file `vsftpd.chroot_list` but don't add anything:

```
sudo touch /etc/vsftpd.chroot_list
```

Modify configurations as following:

```
chroot_local_user=YES
chroot_list_enable=NO
chroot_list_file=/etc/vsftpd.chroot_list
```

Restart vsftpd:

```
sudo service vsftpd restart
```