# UNFS (User-Space Network File System) [![Build Status Image](https://github.com/mu-box/microbox-docker-unfs/actions/workflows/ci.yaml/badge.svg)](https://github.com/mu-box/microbox-docker-unfs/actions)

This is an UNFS Docker image used to launch a UNFS service on Microbox. To use this image, add a data component to your `boxfile.yml` with the `mubox/unfs` image specified:

```yaml
data:
  image: mubox/unfs
```

## UNFS Configuration Options

There are no configuration options for UNFS services, but they work in conjunction with network directories. These are covered in detail in the [Microbox Network Storage documentation](https://docs.microbox.cloud/app-config/network-storage/).

#### Example boxfile.yml with UNFS
```yaml
data.storage:
  image: mubox/unfs

web:
  network_dirs:
    data.storage:
      - path/to/dirA
```

## Help & Support
This is a UNFS Docker image provided by [Microbox](http://microbox.cloud). If you need help with this image, you can reach out to us in the [Microbox Discord](https://discord.gg/MCDdHfy). If you are running into an issue with the image, feel free to [create a new issue on this project](https://github.com/mu-box/microbox-docker-unfs/issues/new).

## License
This project is released under [The MIT License](http://opensource.org/licenses/MIT).
