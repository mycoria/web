# Examples

Easy starters for common use cases.  
Don't forget to lookup the configuration options for more details.


## Connect to Your Server at Home (Behind NAT/FW)

Access your server at home from anywhere, regardless of NAT or firewall:

``` yaml
services:
- name: my-service # This is your service
  url: 'http://my-service.myco/' # For service listening on 0.0.0.0:80 
  friends: true

friends:
- name: alice # This is your laptop
  ip: fd1f:2cd5:6feb:7aa7:d674:1b3c:c82c:dfc
```

See the [configuration reference](/configure) for more details.


## Run Mycoria on a Low End Device

You can tweak Mycoria to make it run smooth on low end devices:

``` yaml
router:
  # Do not relay route announcements to suppres relay traffic.
  stub: true

  # Ask routers not to send route announcements to this router.
  # Reduces load on device.
  # At time of writing, cannot use source routing due to missing information.
  # Only recommended for servers, not clients.
  lite: true
```

See the [configuration reference](/configure) for more details.


## Pure Relay – Without Network Access

If you want to support the Mycoria network, but want to make sure that the Mycoria network cannot access your server in any way, you can simply disable the tun interface:

``` yaml
router:
  # Disables the TUN device, cutting of Mycoria from the network of the device.
  disableTUN: true
```

See the [configuration reference](/configure) for more details.


## Run a Public Service on Mycoria

If you want to run a public service available to all other Mycoria users, you can also advertise it so others can find it through the router dashboard:

``` yaml
services:
- name: My Awesome Service
  description: Awesome service does awesome things.
  url: 'http://awesome-service.myco/'
  public: true
  advertise: true
```

See the [configuration reference](/configure) for more details.


## Use Mycoria Privately

If you're not interested in connecting to other parties within Mycoria, you can keep your device to themselves by adding them as `friends:` and setting `isolate: true`, as well as adding `friends: true` to all your defined services:

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


## Run a Separate Mycoria Network

If you do not want to connect to any other Mycoria router whatsoever, you can do so by creating your own universe:

``` yaml
router:
  universe: my private network
  universeSecret: correct horse battery stable
```

See the [configuration reference](/configure) for more details.
