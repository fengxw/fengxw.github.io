---
layout: post
title: CentOS upgrade to latest stable kernel
modified: 2018-01-10
tags: [linux, kernel, centos]
image:
  feature: abstract-7.jpg
---

## Upgrade

```bash
$ rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
$ rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
$ yum install yum-plugin-fastestmirror
$ yum --enablerepo=elrepo-kernel install kernel-ml
```

## Configure the default startup version of kernel

```bash
$ cat /boot/grub2/grub.cfg | grep menuentry  // look over the list of kernel
$ grub2-set-default 'CentOS Linux (3.10.0-327.el7.x86_64) 7 (Core)'  // set the default startup kernel
$ grub2-editenv list // check result
$ grub2-mkconfig -o /boot/grub2/grub.cfg // enable grub.cfg
```

## Other

### Take a look the kernels had been installed

   ```bash 
   $ rpm -qa | grep kernel
   ```
   
### Clean the useless kernel in the system

   ```bash 
   $ yum remove kernel-3.10.0-327.el7.x86_64
   ```
