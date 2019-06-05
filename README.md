# I2P in Docker

This is the Java I2P router in Docker. Forked from [hkparker/i2p-docker](https://github.com/hkparker/i2p-docker)

# Dockerhub

The link in Dockerhub is [wisicn/i2p-docker](https://hub.docker.com/r/wisicn/i2p-docker)

## Usage

`docker run --name myi2p --restart unless-stopped -d -v ~/.i2p:/var/lib/i2p -p 127.0.0.1:4444:4444 -p 127.0.0.1:7657:7657 -p 127.0.0.1:7658:7658 wisicn/i2p-docker`

### Common problems

If you use Fedora or other selinux enabled OS and get ```mkdir: cannot create directory ‘/var/lib/i2p/.i2p’: Permission denied```, try adding a `:Z` to your volume argument:

```
-v ~/.i2p:/var/lib/i2p:Z
```
As described in the [docker documentation](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label), this should set the selinux labels correctly.

If you want to run I2P webserver(eepsite) in the docker, you must edit the jetty configure file in the docker contain path /var/lib/i2p/i2p-config/eepsite/jetty.xml, Change 127.0.0.1 to 0.0.0.0 in the addListener sectio, and restart I2P router or go to the I2P router console [ConfigClients](http://localhost:7657/configclients) to restart ethe webserver only.
