# A docker for viper framework

This Dockerfile prepares a container to run viper framework, this Dockerfile was a fork from https://github.com/viper-framework/viper-docker to run always from the latest commit.

## Building

```
docker build -t neriberto/viper .
```

## Changelog

### v1

* Fork from https://github.com/viper-framework/viper-docker
* Changes to run from the latest commit

### v2

* Updated Dockerfile to work with the Viper version v2.0-dev (commit: 5cf700761d904d9002a272164735c2ed2b4e0df9)
* Removed pyclamd python library
* Added tools to uncompress files (p7zip-full, unrar)
* Added radare2 (commit: 9e4039ccc320c612a56a5c42f30ee862995e39c0)
