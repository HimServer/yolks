# Yolks

This is fork of Yolks for java for use using azul zulu jdks

Due to this thing is not fully tested, bugs may occer(this only applys on azul zulu prime/zing)

我們這邊提供最新的Azul Zulu jdk(LTS) 給pterodactyl使用

All of these images are available for `linux/amd64` and `linux/arm64` versions, unless otherwise specified, to use
these images on an arm64 system, no modification to them or the tag is needed, they should just work.

## Contributing

When adding a new version to an existing image, such as `java v42`, you'd add it within a child folder of `java`, so
`java/42/Dockerfile` for example. Please also update the correct `.github/workflows` file to ensure that this new version
is tagged correctly.

## Available Images


* [`java`](https://github.com/HimServer/yolks/tree/master/java)
  * [`java8 - Azul Zulu Core`](https://github.com/HimServer/yolks/tree/master/java/8)
    * `ghcr.io/himserver/yolks:java_8` 
  * [`java8 - Azul Zulu Prime`](https://github.com/HimServer/yolks/tree/master/java/8-prime)
    * `ghcr.io/himserver/yolks:java_8-prime`
  * [`java11 - Azul Zulu Core`](https://github.com/HimServer/yolks/tree/master/java/11)
    * `ghcr.io/himserver/yolks:java_11`
  * [`java11 - Azul Zulu Prime`](https://github.com/HimServer/yolks/tree/master/java/11-prime)
    * `ghcr.io/himserver/yolks:java_11-prime`
  * [`java17 - Azul Zulu Core`](https://github.com/HimServer/yolks/tree/master/java/17)
    * `ghcr.io/himserver/yolks:java_17`
  * [`java17 - Azul Zulu Prime`](https://github.com/HimServer/yolks/tree/master/java/17-prime)
    * `ghcr.io/himserver/yolks:java_17-prime`
  * [`java21 - Azul Zulu Core`](https://github.com/HimServer/yolks/tree/master/java/21)
    * `ghcr.io/himserver/yolks:java_21`
  * [`java21 - Azul Zulu Prime`](https://github.com/HimServer/yolks/tree/master/java/21-prime)
    * `ghcr.io/himserver/yolks:java_21-prime`
