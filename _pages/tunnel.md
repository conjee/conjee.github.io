---
title: "tunnel"
excerpt: "A Shadowsocks proxy server"
sitemap: false
permalink: /tunnel.html
---

## Announcements

In response to common slow connection & packet loss issue reported recently, a [KCP-enabled version](https://conjee.info/kunnel) of this service is launched.

Hopefully, it will provide a faster & more stable connection at the cost of a bit more configuration.

Another workaround is to use a CN2 routing service (see the instructions at the end of this page), for which one will always need to pay to a third-party service provider.

## Warnings

1. The proxy server is located in the United States. Violations of Federal Laws and Regulations will lead to an end of this service. Please be mindful not to enagege in any improper activities with this service.

## Configuration

Protocol: `Shadowsocks`

Server Address: `tunnel.conjee.info`

Port: `443`

Encryption Method: `aes-128-cfb`

Key: `tamedowl`

`UDP relay mode` is enabled.

## Clients

`Shadowsocks` is a protocol. You need a client software to use this service. Configuration above just tells the client how to connect to the proxy server I set up.

You can find information of clients for various devices (PCs, Macs, smartphones, etc.) on [this page](https://shadowsocks.org/en/download/clients.html).

Unfortunately, even the official websites and download links of these client software may be inaccessible in censored areas.

Here are backup download links for some clients:

### shadowsocks-windows

Version: `4.0.2`

[Download](https://mega.nz/#!cQZERCJZ!hROefvj2ACjxtMCRbffpTAUbVQ59jZq44_eKxJyCB10)

SHA1: `A8A3E8FFE938712A41875CB6D2218F12A40B2D94`

### ShadowsocksX-NG

Version: `1.5.1`

[Download](https://mega.nz/#!ZJ42mBCA!OF9b9MNbW4ycvje817fkDqY7bWgvjISPJFKWHBJvqXU)

SHA1: `3C6F6A30F43C807681C950CE0B1E6951BE8BE4B7`

### shadowsocks-android

Version: `4.1.7`

[Download](https://mega.nz/#!gMh0kKKK!OGk-itwwPxP8ER10uzhWF-DAdxvp4AEnWnadeqFqq2c)

SHA1: `A0E6E03006E02FAE82B896E0F5184D172852C0F2`

These are not guaranteed to be latest versions. Remember to update once you have access to official download links.

## Support

If you have any problem using this service, contact <tunnel@conjee.info>.

Please note that I may not be able to reply immediately. Your patience is appreciated.

If you are unable to use this service, please include as many details as you can.

Simply telling me "This stuff doesn't work" is not very helpful. Try include information such as:

1. Software Environment: Operating System, Client Software, etc.

2. Network Situation: How are you accessing the Internet? Can you at least reach the server IP address?

3. Configuration you are using.

4. Logs.

## [Optional] High-Quality Connection through China Telecom's Next Generation Network

The basic settings should be sufficient for web searching. However, you can get better connection quality by using China Telecom's Next Generation Network, CN2. It can greatly reduce package loss rate and optimize bandwidth. I have no problem streaming 1080p Youtube videos with this tweak.

China Telecom users can order `国际精品网` by calling customer service to use CN2 in some provinces. The price is 50 RMB per month if I remember it correctly. And you can only use it with appointed ADSL account.

You can also use [VnetLink](https://vnet.link/?rc=21400)'s vxTrans service to route your Shadowsocks connection through their CN2 server. This works well for most users in China as long as they have a good connection to VnetLink's CN2 server.

