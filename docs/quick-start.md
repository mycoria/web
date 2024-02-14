# Quick Start

If you just want to plunge into it and try it, here is the fastest way:

### Download Binary

[Windows amd64](https://github.com/mycoria/mycoria/releases/latest/download/mycoria_windows_amd64.exe) [arm64](https://github.com/mycoria/mycoria/releases/latest/download/mycoria_windows_arm64.exe)  
[Linux amd64](https://github.com/mycoria/mycoria/releases/latest/download/mycoria_linux_amd64) [arm64](https://github.com/mycoria/mycoria/releases/latest/download/mycoria_linux_arm64)

_Or, [build from source](https://github.com/mycoria/mycoria?tab=readme-ov-file#building) instead._

!!! tip "More platforms are planned, help is welcome!"

!!! info "Required Dependency for Windows"

    Mycoria requires WinTun. [Download it here](https://www.wintun.net/) and place `wintun.dll` in the same directory as mycoria.exe

### Generate Config

``` sh
mycoria config generate XX # Replace XX with your country code.
```

!!! info "Why does Mycoria need my country code?"

    It's a vital part of the scalable routing concept.  
    [Read more about it here.](/concept/#scalable-routing)
    
    If you pick an incorrect one, it will undermine _your_ routing performance.

### Run it!

``` sh
mycoria run --config /path/to/config.yaml
```

!!! info "Required Setup for .myco Domains on Linux"

    Linux requires some extra setup for .myco domains to work. Read how to do this in [this install page section](/install/#dns-on-linux).
