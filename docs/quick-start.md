# Quick Start

If you just want to plunge into it and try it, here is the fastest way:

### Download Binary

- [Linux (amd64)](https://github.com/mycoria/mycoria/releases/download/v0.0.1/mycoria_linux_amd64)
- [Build from source](https://github.com/mycoria/mycoria?tab=readme-ov-file#building)

!!! tip "More platforms coming soon!"

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
