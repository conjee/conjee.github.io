---
layout: post
title: "Binance Desktop Proxy Settings"
categories: notes
description: "Steps to configure network proxy settings for Binance desktop app."
---

## The Command Line Trick to Set Proxy Server

I can't find proxy server settings within Binance Desktop's GUI. But the Electron app accepts such settings through [command line arguments](https://www.electronjs.org/docs/api/command-line-switches), e.g.:

    /Applications/Binance.app/Contents/MacOS/Binance --proxy-server="socks5://proxy-host:1080"

There're many ways to "redirect" the connections, but I found this suitable for my needs as it's easy to set up and doesn't affect other apps. I use it with ssh dynamic port fowarding:

    ssh -D 1080 -q -C -N -f my-proxy-server
    /Applications/Binance.app/Contents/MacOS/Binance --proxy-server="socks5://localhost:1080"

## Using a PAC File

I also find it handy to use a PAC file to redirect connections to some of the domains but not the others.

Example PAC file content:

```
function FindProxyForURL(url, host) {
    if (dnsDomainIs(host, "www.binance.com") || dnsDomainIs(host, "www.binance.me")) {
        return "SOCKS5 localhost:1080";
    } else {
        return "DIRECT";
    }
}
```

`--proxy-pac-url=` argument unfortunately stopped supporting local files (`file://...`), but there's a simple workaround -- loading the file as an HTTP response:

    /Applications/Binance.app/Contents/MacOS/Binance --proxy-pac-url='data:application/x-javascript-config;base64,'$(base64 $PAC_FILE_PATH)

