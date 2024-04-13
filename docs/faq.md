# FAQ

## Do I Need To Configure IANA IPs?

No, IANA IPs are optional!

IANA IPs are just useful so that other Mycoria routers can connect to your router via the Internet. This also enables other routers to automatically optimize the network by connecting directly to your router if there is a lot of demand.



## How Can I Use Mycoria Privately?

If you're not interested in connecting to other parties within Mycoria, you can keep your device to themselves by adding them as `friends:` and setting `isolate: true`, as well as adding `friends: true` to all your defined services.

Config excerpt:

``` yaml
router:
  isolate: true

services:
- name: ping
  url: 'icmp6:'
  friends: true

friends:
- name: alice
  ip: fd1f:2cd5:6feb:7aa7:d674:1b3c:c82c:dfc
```

This way, you can still use the global Mycoria network for routing, connectivity and relaying your own traffic, but you do not send any traffic to any other Mycoria routers, and do not allow any other routers to access your defined services.

See the [configuration reference](/configure) for more details.



## Can I Run a Separate Mycoria Network?

If you do not want to connect to any other Mycoria router whatsoever, you can do so by creating your own universe:

``` yaml
router:
  universe: my private network
  universeSecret: correct horse battery stable
```

See the [configuration reference](/configure) for more details.
