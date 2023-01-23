# V2ray single user connection

## The issue description

V2ray ,basically, is set of network protocols to bypass internet restrictions. It's is designed and implemented by some PRC people to bypass GFW.  
And of course, Iran regime **LOVES** the restriction idea of GFW; therefore tries to be like his *big brother*, awww... CUTE!!! And **we** try to be like those who fight against this BS.

Really **important** note about these protocols is that they don't provide a **Virtual Private Network** for you, just a traffic proxy :)

However, besides these protocols are extremely depended on ISPs rules (a protocol may work on one ISP but not the other), for service provider there's another issue as well, **Accounting**.  
V2ray panel ,aka `x-ui`, provide basic accounting (in sense of creating, bandwidth limitation and such) however does not provide any possible way to *limit* user counts per account.

> For instance, when an `VLESS` account created, it could be easily distributed by the end-user to many as he wants. Which might sound not too much of a problem right?? Well, no, it is big one actually.

Because in such manner, `VPS`'s traffic could be multiplied by huge number and over what that had been anticipated by maintainer. Which ultimately causes being easier detected by edge-firewalls as a problem. (Much more work for maintainer to fix it)

***So, What is the solution?***

## The solution

Well, something should we consider is that most V2ray protocols like (VLESS and VMESS) listens on customizable ports for incoming connections.  
> For instance, User1's VLESS account listens on 5900 and User2's VMESS account listens on 8900.

With this property, the issue maps to such problem ====> How we can limit incoming connections per **port**?  
> In the other words, how to make sure only **one public IP** is connected to our desired **port**?

Well, V2ray **does not** provide this functionality, but **Linux** does :)

Our old friend `iptables`, helps us to do so.

In short, `ipatables` is an old (by some even deprecated, and replaced by `nftables` or `firewalld`) firewalling framework for `Linux`.
Despite being used for so many years (like **Two Decades**), many robust applications still uses its feature for finding solutions for specific scenarios. like our other friend **Docker**.

So, how `iptables` is going to help us to solve this issue?  
Well, one the cool feature about `iptables` is having many modules, one of which is `connlimit` module. :)

You could check `iptables`'s `connlimit` man page for full understating of it.

Well, I'm not going to tell exactly which commands to use (because where the fun goes then, right? :) ), but I will mention 2 important notes:

***Remember***,

1. Some V2ray protocols (like VLESS & VMESS) will establish multiple connections to server to provide faster service.
    > So limiting connections to only one connection will not work. (find the sweet spot)

2. Your working with **Public IPs**, so don't forget the **netmask**.

A suggestion btw, try a `bash` script to set new user's settings to system, which anyone with not so much experience with `Linux` could use it.

Thats's it,
Thanks for reading, have fun! :)
