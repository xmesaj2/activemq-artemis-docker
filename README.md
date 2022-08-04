# ACTIVELY MAINTAINED BUT NOT ACTIVELY SUPPORTED FOR OTHER USERS

## (Welcome but don't expect quick answers to questions or feature requests)

This is a fork of ["qoricode"](https://github.com/qoricode/activemq-artemis-docker) repo for running using OpenJDK Zulu distribution, which supports arm64 (Apple Silicon).
I have also broken most of Docker Hub stuff as I don't need all of this personally.

Runs Zulu OpenJDK 18 and Artemis 2.23.1.

### Build

```console
cd src && docker build --build-arg ACTIVEMQ_ARTEMIS_VERSION=2.23.1 --build-arg BASE_IMAGE=azul/zulu-openjdk-debian:18 -t xmesaj2/activemq-artemis:2.23.1 .
```

### Run

```console
docker run --rm -it  -p 1883:1883/tcp -p 5445:5445/tcp -p 5672:5672/tcp -p 61613:61613/tcp -p 61616:61616/tcp -p 8161:8161/tcp -p 9404:9404/tcp xmesaj2/activemq-artemis:2.23.1 
```

http://127.0.0.1:8161/console

### Original note

Since the author of the ["vromero"](https://github.com/vromero/activemq-artemis-docker) image - well done to him - stopped maintaining it at v2.16 I forked it here and will release new Artemis versions at [Docker Hub](https://hub.docker.com/r/qoricode/activemq-artemis) as they are released on "reasonable endeavours". Note I'm not planning to maintain the Alpine ones, only the Debian ones.

Also fixed a few minor issues (from my point of view) -

- Old 2016 version of ca-certificates was baked in - now pulls latest.
- Internet fetch operations were muted during the build - now reports e.g. certificate issues during build and pulls artemis signing keys via https.
- ENABLE_JMX and ENABLE_JMX_EXPORTER would be enabled on any value e.g. false, now will only be enabled if == true.
- ENABLE_JMX_EXPORTER would activate ENABLE_JMX when not actually needed - now independent of each other.
  - Note ENABLE_JMX actually enables remote, anonymous JMX access. (Local) JMX is enabled via broker.xml and on by default.

## License

View [license information](http://www.apache.org/licenses/LICENSE-2.0) for the software contained in this image.
