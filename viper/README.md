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
* [Yara](https://github.com/VirusTotal/yara) (from commit: 27e385271f9084a2c127f2ca5aaab8e800f6884c)
* [Radare2](https://github.com/radare/radare2) (from commit: 8cb110efa3fd1fada8bb3f770fd2d3536a357bdd)
