---
title: "tunnel"
excerpt: "A Shadowsocks proxy server"
sitemap: false
permalink: /tunnel.html
---

## Announcements

In response to common slow connection & packet loss issue reported recently, a [KCP-enabled version](https://conjee.info/kunnel) of this service is launched.

Hopefully, it will provide a faster & more stable connection at the cost of a bit more configuration.

Another workaround is to use a CN2 routing service (see the instructions below), for which one often need to pay to a third-party service provider.

## Warning

The proxy server is located in the United States. Violations of Federal Laws and Regulations will lead to an end of this service. Please be mindful not to enagege in any improper activities with this service.

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

## Support

If you have any problem using this service, contact tunnel@conjee.info.

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

After [Registration](https://vnet.link/?rc=21400), create a connection point like this:

![Connection Point Setup]({{ site.url }}{{ site.baseurl }}/assets/images/tunnel/connection-point-setup.png)

Then change your client settings accordingly:

![Client settings CN2]({{ site.url }}{{ site.baseurl }}/assets/images/tunnel/client-settings-cn2.png)

I recommend you to create a new server profile for this and keep the old one. This way, you can switch to the original settings flexibly to minimize data usage.
