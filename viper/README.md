# A docker for viper framework

This Dockerfile prepares a container to run viper framework, this Dockerfile was a fork from https://github.com/viper-framework/viper-docker to run always from the latest commit.

## Building

```
docker build -t neriberto/viper .
```

### Apps bundle

* [Viper](https://github.com/viper-framework/viper) version v2.0-dev (from commit: 5cf700761d904d9002a272164735c2ed2b4e0df9)
* Tools to uncompress files (p7zip-full, unrar)
* Added exiftool
* [Yara - version 3.8.0](https://github.com/VirusTotal/yara)
* [Radare2 - version 2.8.0](https://github.com/radare/radare2)
