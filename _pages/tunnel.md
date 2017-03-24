---
title: "tunnel"
excerpt: "A Shadowsocks proxy server for academic use only."
sitemap: false
permalink: /tunnel.html
---

## News

The server went down at 2017-01-07 15:32:29 UTC due to a software failure. It is restarted on 2017-01-10 UTC.

~~An update from the upstream will fix the bug soon. Meanwhile, avoid visiting any site with a long domain name.~~

Update complete on 2017-01-22. Bug fixed.

## Warning

1. This proxy server is for academic use only!
2. You are *NOT* allowed to share any information provided by this page.

## Configuration

Protocol: Shadowsocks

Server Address: `tunnel.conjee.info`

Port: `11985`

Encryption Method: *aes-128-cfb*

Key: `yiban666`

[One Time Auth](https://shadowsocks.org/en/spec/one-time-auth.html) is supported.

## Clients

### For Windows

#### shadowsocks-windows

Download [here](https://github.com/shadowsocks/shadowsocks-windows/releases)

#### How-to

1. Add this server using the configuration above
2. Update PAC file from GFWList
3. Enable System Proxy
4. Make sure your browser's proxy is set to use system's default settings

### For Android

#### shadowsocks-android

Download [here](https://github.com/shadowsocks/shadowsocks-android/releases)

## [Optional] Higher Connection Quality through China Telecom's Next Generation Network

The basic settings should be sufficient for web searching. However, you can get better connection quality by using China Telecom's Next Generation Network, CN2. It can greatly reduce package loss rate and optimize bandwidth. I have no problem streaming 1080p Youtube videos with this tweak.

China Telecom users can order `国际精品网` by calling customer service to use CN2 in some provinces. The price is 50 RMB per month if I remember it correctly. And you can only use it with appointed ADSL account.

You can also use [VnetLink](https://vnet.link/?rc=21400)'s vxTrans service to redirect your Shadowsocks connection through their CN2 server. This works well for most users in China as long as they have a good connection to VnetLink's CN2 server. The price is 1 RMB per GB data usage. This is the method I am using. It's cheaper and accessible everywhere.

After [Registration](https://vnet.link/?rc=21400), create a connection point like this:

![Connection Point Setup]({{ site.url }}{{ site.baseurl }}/assets/images/tunnel/connection-point-setup.png)

Then change your client settings accordingly:

![Client settings CN2]({{ site.url }}{{ site.baseurl }}/assets/images/tunnel/client-settings-cn2.png)

I recommend you to create a new server profile for this and keep the old one. This way, you can switch to the original settings flexibly to minimize data usage.
