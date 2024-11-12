# dnsrouter

<p>
  <img src="https://img.shields.io/badge/dnsrouter-0.0.9-green.svg?style=for-the-badge">
  <a href="https://hub.docker.com/repository/docker/jc21/dnsrouter">
    <img src="https://img.shields.io/docker/stars/jc21/dnsrouter.svg?style=for-the-badge">
  </a>
  <a href="https://hub.docker.com/repository/docker/jc21/dnsrouter">
    <img src="https://img.shields.io/docker/pulls/jc21/dnsrouter.svg?style=for-the-badge">
  </a>
</p>

This is a docker image running the [dnsrouter](https://github.com/jc21/dnsrouter) binary.

The following architectures are supported for all images:

- amd64
- arm/v7
- arm64

### Usage:

```
docker run jc21/dnsrouter \
  -v /path/to/dnsrouter-config.json:/dnsrouter-config.json
```

### Dnsrouter Config

The default config written into the docker image is [defined here](files/dnsrouter-config.json)
however you will definitely want to create your own configuration and mount it into your container instead.

See the [dnsrouter project](https://github.com/jc21/dnsrouter) for configuration.
