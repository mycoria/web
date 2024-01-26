# Install

## Packages

_We haven't packaged Mycoria yet for any platform. If you want help out, it is much appreciated._

## Manual Install

### Linux

``` sh
# Create directory and download binary.
mkdir /opt/mycoria
wget https://github.com/mycoria/mycoria/releases/download/v0.0.1/mycoria_linux_amd64 -O /opt/mycoria/mycoria
chmod +x /opt/mycoria/mycoria

# Generate config file.
/opt/mycoria/mycoria config generate XX # Replace XX with your country code.

# Install and enable systemd service
curl https://raw.githubusercontent.com/mycoria/mycoria/master/packaging/mycoria.service | sudo tee 
systemctl enable mycoria
systemctl start mycoria
journalctl -fu mycoria
```

_Why does Mycoria need your country code? [It helps with routing scalability.](/concept/)_
