---
title: "kunnel"
excerpt: "A KCP-enabled Shadowsocks proxy server"
sitemap: false
permalink: /kunnel.html
---

## Announcements

This is a KCP-enabled version of the original [tunnel](https://conjee.info/tunnel) service.

Hopefully, it will provide a faster & more stable connection at the cost of a bit more configuration.

## Warnings

1. The proxy server is located in the United States. Violations of Federal Laws and Regulations will lead to an end of this service. Please be mindful not to enagege in any improper activities with this service.

2. Higher data & battery consumption is expected beacuse of KCP's nature. Be careful if you are using this on a mobile device.

## Configuration

Protocol: `Shadowsocks over KCP`

Server Address: `kunnel.conjee.info`

UDP Port: `443`

Shadowsocks Encryption Method: `aes-128-cfb`

SHadowsocks Encryption Key: `tamedowl`

KCP Client parameters: `--dscp 46 --key "tamedowl"` (Use the default value for others)

## Clients

To use KCP, additional tools may be necessary on some platforms.
