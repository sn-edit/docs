# Getting Started

We support every major platform but only the 64 bit distributions. Please choose your platform below, let it be macOS, Linux or Windows.

Follow the instructions below to set sn-edit up!

## Download

<!-- tabs:start -->

#### ** macOS **
Download the binary
```bash
$ wget https://github.com/sn-edit/sn-edit/releases/download/v0.2/sn-edit-darwin-amd64 -O /usr/local/bin/sn-edit
$ chmod +x /usr/local/bin/sn-edit
$ sn-edit --version # should print sn-edit v0.2 6582622 darwin/amd64
```

If you prefer, you can also install it using homebrew
```bash
$ brew install sn-edit/stable/sn-edit
$ sn-edit --version # should print sn-edit v0.2 6582622 darwin/amd64
```

#### ** Linux **
Download the binary
```bash
$ wget https://github.com/sn-edit/sn-edit/releases/download/v0.2/sn-edit-linux-amd64 -O /usr/local/bin/sn-edit
$ chmod +x /usr/local/bin/sn-edit
$ sn-edit --version # should print sn-edit v0.2 6582622 linux/amd64
```

If you prefer, you can also install it using homebrew
```bash
$ brew install sn-edit/stable/sn-edit
$ sn-edit --version # should print sn-edit v0.2 6582622 linux/amd64
```

#### ** Windows **
1. Download the binary for Windows on the [releases page](https://github.com/sn-edit/sn-edit/releases/latest).
2. Create a folder in your user folder called `sn-edit`. So the path would look like this: `C:\Users\<your-username>\sn-edit`
3. Put the downloaded exe file into this folder and name it `sn-edit`, this means you should have one exe file there with the name `sn-edit.exe`
4. Please add your path `C:\Users\<your-username>\sn-edit` to your **Path (environment variable)** under **System variables** following the guide in step 5 
5. Follow the instructions laid out in this [article](https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/)
6. The path you will have to add is the same as above `C:\Users\<your-username>\sn-edit` (replace <your-username> with your own value)
7. Open a cmd and write `sn-edit --version` to check if everything works. The output should be something like this: `sn-edit version v0.2 6582622 windows/amd64`

<!-- tabs:end -->

## Configuration
You will need to setup a config file for sn-edit to work properly. The app has a lot of parameters, which are making it
difficult to provide them in a format of flags.

sn-edit will look for a config file named `.sn-edit.yaml` either in the current directory in a folder `_config` or in your
home folder under `$HOME/.sn-edit.yaml`

For a detailed description of the configuration options, please visit [Configuration Instructions](configuration/README.md)