---
title: LXD / LXC
description: 
published: true
date: 2020-08-15T10:51:41.062Z
tags: 
editor: markdown
dateCreated: 2020-06-17T13:48:08.673Z
---

![linux_containers_logo[1].png](/linux_containers_logo[1].png =100x100){.align-left}
is an operating-system-level virtualization method
for running multiple isolated Linux systems on a control host using a single Linux kernel.

---

# Overview
## LXC
LXC is a userspace interface for the Linux kernel containment features.
Through a powerful API and simple tools, it lets Linux users easily create and manage system or application containers.

---

## LXD
LXD is a next generation system container manager. It offers a user experience similar to virtual machines but using Linux containers instead.
It's image based with pre-made images available for a wide number of Linux distributions and is built around a very powerful, yet pretty simple, REST API.

---

# Commands
## Managing
```bash
script
```
---

## Creating
Search all LXC images
```bash
lxc image list images:
# use grep to select image name
```

```bash
lxc launch images:[imageID] {containerName}
```

```bash
script
```
---

## Maintaining
push file from host into the container:
```bash
lxc file push /host/file(source) containername/destination
```

```bash
script
```
---

## Migrating
```bash
script
```

---