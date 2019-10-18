---
layout: post
title: "Wireshark Permission Issues on Clear Linux"
categories: notes
description: "Permission issues with Wireshark ran as a non-root user can be fixed by setting dumpcap permissions and privileges."
---

## The Problem

I installed Wireshark on a Clear Linux instance with the command:

    sudo swupd bundle-add wireshark

I got the following error when I was trying to capture on a network interface as a non-root user:

> The capture session could not be initiated on ...
> Please check to make sure you have sufficient permissions.
> ...

![Error Screenshot](/assets/wireshark-permission-issues-on-clear-linux/error.png)

## A Solution

I followed the steps on [this page](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods), which apply to a more general situation.

In the case of Clear Linux, the group `wireshark` should have already been created after the installation. The following steps are necessary.

Add yourself to the group:

    sudo gpasswd -a $USER wireshark

Change the group of `/usr/sbin/dumpcap` to `wireshark`:

    sudo chgrp wireshark /usr/sbin/dumpcap

Restrict access:

    sudo chmod o-rx /usr/sbin/dumpcap

Set network privileges:

    sudo setcap cap_net_raw,cap_net_admin+eip /usr/sbin/dumpcap
