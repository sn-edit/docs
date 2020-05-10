# Getting Started

We provide releases for MacOS, Windows and Linux. Pick the version you would like to download.
Choose the platform.

We provide support for 64 bit distributions only, let it be Linux, macOS or Windows. You can get the source code
and compile it if you want to.

## Download

<!-- tabs:start -->

#### ** macOS **
Download the binary
```bash
$ wget https://github.com/sn-edit/sn-edit/releases/download/v0.2/sn-edit-darwin-amd64 -O /usr/local/bin/sn-edit
$ chmod +x /usr/local/bin/sn-edit
$ sn-edit version # should print sn-edit v0.2
```

If you prefer, you can also install it using homebrew
```bash
$ brew install sn-edit/stable/sn-edit
$ sn-edit version # should print sn-edit v0.2
```

#### ** Linux **
Download the binary
```bash
$ wget https://github.com/sn-edit/sn-edit/releases/download/v0.2/sn-edit-linux-amd64 -O /usr/local/bin/sn-edit
$ chmod +x /usr/local/bin/sn-edit
$ sn-edit version # should print sn-edit v0.2
```

If you prefer, you can also install it using homebrew
```bash
$ brew install sn-edit/stable/sn-edit
$ sn-edit version # should print sn-edit v0.2
```

#### ** Windows **
Download the binary for Windows on the [releases page](https://github.com/sn-edit/sn-edit/releases/latest).

<!-- tabs:end -->

## Configuration
You will need to setup a config file for sn-edit to work properly. The app has a lot of parameters, which are making it
difficult to provide them in a format of flags.

sn-edit will look for a config file named `.sn-edit.yaml` either in the current directory in a folder `_config` or in your
home folder under `$HOME/.sn-edit.yaml`

For a detailed description of the configuration options, please visit [Configuration Instructions](configuration/README.md)