---
layout: post
title: Mirror for remote samba sharing folder
category: ops
tag: [ops,samba,smb,linux,windows,puppet,rundeck]
shortinfo: sync the remote samba folder to local , and share with them by samba service.

---

# Mirror for remote samba sharing folder
It's very slow to access the samba for which is shared from offshore team with very low speed. so we try to create an mirror for these files.

* protocol type : [samba](http://en.wikipedia.org/wiki/Samba_(software)
* remote machine: windows (only able to read)
* local machine : linux (Oracle Linux 6)

## mount the samba driver by puppet

install packages for samba client & server

```
package { 'samba':
        ensure => installed,
}
package { 'cifs-utils':
        ensure => installed,
}
```



```
# create mount driver
file {'/mnt/MOUNT_NAME':
      ensure => directory ,
      mode => 755,
}

 mount { '/mnt/MOUNT_NAME':
      ensure  => mounted,
      device  => 'SRC_FOLDER(such as //10.180.X.XXX/XX/)',
      fstype  => 'cifs',
      options => 'rw,username=USER,password=PASSWORD',
       require => [ File['/mnt/MOUNT_NAME'] , Package['cifs-utils'] ,  Package['samba'] ],
    }

```

## rsync the folder by rundeck schedule

yaml config

```
- id: c6c89d9c-7844-495f-90b0-7ff2f18ac3bc
  project: env
  schedule:
    time:
      hour: '*'
      minute: 0/15
      seconds: '0'
    month: '*'
    year: '*'
    weekday:
      day: '*'
  loglevel: INFO
  sequence:
    keepgoing: false
    strategy: node-first
    commands:
    - exec: rsync -avvh --progress /mnt/MOUNT_NAME /var/mirror
      description: rsync from  /mnt/MOUNT_NAME  to /var/mirror
  description: rsync  /mnt/MOUNT_NAME
  name: rsync_smb_MOUNT_NAME
  notification:
    onfailure:
      recipients: XXXX@mail.com
    onsuccess:
      recipients: XXXX@mail.com
  uuid: c6c89d9c-7844-495f-90b0-7ff2f18ac3bc
  nodefilters:
    dispatch:
      threadcount: 1
      keepgoing: false
      excludePrecedence: true
      rankOrder: ascending
    filter: 'name: XXX.YYY.com'
  group: GROUPA/GROUPB
```


## create local samba server for sharing

add content in /etc/samba/smb.conf

```
[mirror]
        comment = samba mirror
        path = /var/mirror
        browseable = yes
        guest ok = yes
        guest account = ACCOUNT_NAME
        writable = no

```

then restart the service

```
sudo /etc/init.d/smb restart
```
