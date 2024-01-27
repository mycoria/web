# Install

## Packages

_We haven't packaged Mycoria yet for any platform. If you want help out, it is much appreciated._

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
