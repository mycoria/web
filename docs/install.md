# Install

## Packages

_We haven't packaged Mycoria yet for any platform. If you want to help out, it is much appreciated._

## Manual Install

!!! tip "More platforms coming soon!"

### Linux (amd64)

``` sh
# Create directory and download binary.
mkdir /opt/mycoria
wget https://github.com/mycoria/mycoria/releases/download/v0.0.1/mycoria_linux_amd64 -O /opt/mycoria/mycoria
chmod +x /opt/mycoria/mycoria

# Generate config file.
/opt/mycoria/mycoria config generate XX | tee /opt/mycoria/config.yaml # Replace XX with your country code.

# Install and enable systemd service
curl https://raw.githubusercontent.com/mycoria/mycoria/master/packaging/mycoria.service | sudo tee /etc/systemd/system/mycoria.service
systemctl enable mycoria # Start at boot.
systemctl start mycoria # Start now.
journalctl -fu mycoria # Live-view logs.
```

!!! info "Why does Mycoria need my country code?"

    It's a vital part of the scalable routing concept.  
    [Read more about it here.](/concept/#scalable-routing)
    
    If you pick an incorrect one, it will undermine _your_ routing performance.

### DNS on Linux

In order to use `.myco` domains, you need to tell Linux to resolve `.myco` using Mycoria.

As there are so many different systems and configuration options, help here is much appreciated.  
(This is such a mess on Linux - we probably won't try to auto-configure this until it gets better.)

#### Option 1: systemd-networkd

Create this file

``` sh
/etc/systemd/network/mycoria.network
```

with the following contents:

``` ini
[Match]
Name=mycoria

[Network]
DNS=fd00::b909
Domains=~myco
```

To make sure the changes are picked up do:

```sh
sudo networkctl reload
```

#### Option 2: systemd-resolved

Create this file

``` sh
/etc/systemd/resolved.conf.d/mycoria.conf
```

with the following contents:

``` ini
[Resolve]
DNS=fd00::b909
Domains=~myco
```

To make sure the changes are picked up do:

```sh
sudo systemctl restart systemd-resolved
```

Note: If you have another global resolver configured, make sure it has `Domains=~.` set for better compatibility. Otherwise all queries might be first routed to mycoria and then your other resolver. It still works, but you loose a couple milliseconds.

#### Option 3: NetworkManager

``` sh
nmcli connection modify mycoria ipv6.dns "fd00::b909"
nmcli connection modify mycoria ipv6.dns-search "myco"
nmcli connection modify mycoria ipv6.dns-options "inet6 timeout:1 attempts:1"
nmcli connection modify mycoria ipv6.dns-priority "1000"

# Check interface settings with:
nmcli connection show mycoria
# Check full status with
nmcli
```

If this does not work or you have multiple mycoria interfaces in nmcli, try resetting the NetworkManager interface settings for mycoria:

``` sh
nmcli connection delete mycoria
sudo rm /etc/NetworkManager/system-connections/mycoria.nmconnection
```

#### Option 4: IPv6 Router Advertisements (ND/SLAAC)

Mycoria sends router advertisements that advertise the DNS server (RDNSS) and the `.myco` domain (DNSSL).  
If you can make your Linux accept these, everything _might_ auto-configure.

Starting point:  

``` sh
sudo sysctl -w net.ipv6.conf.mycoria.accept_ra=1
```

_The rest is up to you._

#### Option 5: Portmaster

If you are using [Portmaster](https://safing.io/), you can simply add this to the configured DNS Servers:

``` urlencoded
dns://[fd00::b909]?name=Mycoria&search=myco&search-only
```
