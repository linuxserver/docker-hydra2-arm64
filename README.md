[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/theotherp/nzbhydra2
[hub]: https://hub.docker.com/r/lsioarmhf/hydra2-aarch64/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/hydra2`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/hydra2-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/hydra2-aarch64.svg)](https://microbadger.com/images/lsioarmhf/hydra2-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/hydra2-aarch64.svg)](http://microbadger.com/images/lsioarmhf/hydra2-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/hydra2-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/hydra2-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-hydra2)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-hydra2/)

_NZBHydra 2_ is a meta search application for NZB indexers, the "spiritual successor" to _NZBmegasearcH_, and an evolution of the original application _[NZBHydra](https://github.com/theotherp/nzbhydra)_ . It provides easy access to a number of raw and newznab based indexers. 

The application NZBHydra 2 is currently in its early stages and is in active development. Be wary that there may be some compatibility issues for those migrating from V1 to V2, so ensure you back up your old configuration before moving over to the new version.

[![hydra](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/hydra-icon.png)][appurl]

## Usage

```
docker create --name=hydra2 \
-v <path to data>:/config \
-v <nzb download>:/downloads \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 5076:5076 lsioarmhf/hydra2-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 5076` - the port(s)
* `-v /config` - Where hydra2 should store config files
* `-v /downloads` - NZB download folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone EG. Europe/London

It is based on ubuntu bionic with s6 overlay, for shell access whilst the container is running do `docker exec -it hydra2 /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARM64 VERSION`

The web interface is at `<your ip>:5076` , to set up indexers and connections to your nzb download applications.


## Info

* To monitor the logs of the container in realtime `docker logs -f hydra2`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' hydra2`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/hydra2-aarch64`

## Versions

+ **22.01.19:** This image is deprecated. Please use the multi-arch images at linuxserver/hydra2
+ **18.08.18:** Bump java version to 10, (bionic currently refers to it as version 11).
+ **10.08.18:** Rebase to ubuntu bionic.
+ **15.04.18:** Change to port 5076 in the Dockerfile.
+ **12.01.18:** Initial Release.
