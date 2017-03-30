# A docker for viper framework

This Dockerfile prepares a container to run viper framework, this is a fork from https://github.com/viper-framework/viper-docker to run always from the latest commit.

## Building

```
docker build -t neriberto/viper .
```

## Running from Windows desktop

Below an example to run in a Windows desktop for development and tests (Don't forget to stop any antimalware, like Windows Defender).

```
docker run --rm -p 9090:9090 -it -v viper:/home/viper/.viper/ neriberto/viper
```

## Changelog

### v1

* Fork from https://github.com/viper-framework/viper-docker
* Changes to run from the latest commit
