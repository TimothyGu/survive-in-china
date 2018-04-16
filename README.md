# Surviving in China

It is not easy being a software developer based in China, due to the multifaceted and multilayered restrictions the government has placed on the Internet (through a system known as the Great Firewall, or GFW for short). It is even more difficult to be a software developer not based in China, but is in China for one reason or another.

Specifically for software developers, however, there are many solutions available to solve or at least alleviate these problems. In this document, I will attempt to first describe the nature and extent of the Internet restrictions, and then exhibit the currently available solutions.

## How Internet Is Like in China

In China, you may observe:

- Slow connection to servers overseas
- Impossible to connect to certain services overseas (i.e. "blocked")

Despite several attempts, there are no exhaustive lists of websites blocked available. However, the following services are almost always denied access within the country:

- Google
- Facebook
- Twitter
- Snapchat
- Instagram

The following websites, notably, actually work as of now:

- Bing
- GitHub

## How the GFW Works

- DNS poisoning.

  When you try to visit `google.com`, your browser first make a query to a DNS server asking for the IP address corresponding to `google.com`. However, a DNS query is unencrypted, so the Wall is able to intercept the query and return an invalid IP address rather than the correct one.

- HTTP sniffing.

  Vanilla HTTP requests are not encrypted, so the Wall is able to see exactly what you request the server for. When the request contains `google.com`, for example, the Wall will automatically stop the connection from being created.

- HTTPS interruption.

  Due to the TLS encryption incorporated in HTTPS, the Wall can't sniff the content of an HTTPS request to a specific server. However, they can obtain a list of all Google IP blocks, for example, and interrupt all HTTPS connections to those IPs.

## What Works

None of these solutions is a panacea against Internet restrictions in China. In fact, a server *will* get blocked when too many people use it and thusly make it easier to detect. However, they still work if you are able to slip under the radar.

- VPN (L2TP+IPSec; IKEv2 might work too but I never tested).
  
  VPNs work by tunneling all network packets through a server with access to free Internet. However, the government has recently announced sanctions against VPNs. Even though the sanction is effective next year, crackdown against several public and popular VPNs has already started.
  
  Despite that, VPNs are still the most reliable way of tunneling to a server overseas. If you have the time and a server available, setting up your own VPN may be a worthwhile venture, as it has the largest chance of slipping under the Wall while providing a reliable connection.

  After you have obtained a VPN, be sure to use its IP address instead of domain name when setting it up on your devices; otherwise it may be susceptible to DNS poisoning attack (as described above). If you are already in China, there are several (western) websites online that offer domain-to-IP services unencumbered by DNS poisoning.
  
  <!-- TODO: link tutorials -->

- Clean `hosts` file + HTTPS

  A [`hosts` file][] in a system allows DNS resolution without contacting a DNS server, thus avoiding DNS poisoning. On the other hand, HTTPS connections allow

- HTTPS proxy (as in, HTTP(S) proxy over TLS).

  Unlike its unencrypted brother HTTP proxy, HTTPS proxies are usually able to evade detection due to their scrambled traffic.

- SOCKS proxy.

  If you have SSH access to a server that is not blocked, you can easily set up a SOCKS tunnel. SOCKS proxies work much like VPNs in that they tunnel everything, not just HTTP(S) requests, but can be pretty slow. I wrote a script to allow load-balancing among different SOCKS proxies which alleviate the problem somewhat, but in general this solution should be reserved for 

## What Does Not work

- Unencrypted HTTP proxy.

  An unencrypted HTTP proxy is, well, unencrypted, so the GFW can see an attempt to use proxies and stop it.

- Tor without your own entrance point.

  Unfortunately, the Wall has figured out how to detect Tor connections and stop them, so unless you are using a custom server as entrance point it is unlikely to work.

## When Nothing Works

When all of the above solutions do not work or are not available, try alternatives that are available in China. 

- Google -> Bing.

  Yes I know, Bing sucks. But it is still much better than the homegrown Chinese search engine, Baidu, especially when searching non-Chinese resources.

- Google Maps -> Baidu Maps or Bing Maps.

  Baidu Maps is in Chinese, but is generally regarded as fairly authoritative among my Chinese friends. If you are not okay with the language, Bing Maps should work as well.

- Gmail and Google Drive

  If you have stuff on one of these services you need to access, and cannot access Google, sorry you're toast. However, Chinese homegrown solutions like [Baidu Wangpan](https://yun.baidu.com/) work, and [126 Mail](https://www.126.com/) works pretty well as far as I can tell.
