### Introducing `bluefin-cli`
**Note:** This feature is under heavy development. If all of this is confusing to you ignore it. :smiley: 

![image|690x376](upload://3k18RiX3TZMBkmp77bprKCl1ygI.jpeg)

`ujust bluefin-cli` will install `bluefin-cli`, Bluefin's opt-in command line experience. It is a dedicated toolbox container that is designed to give the user access to as much software as possible while providing a modern Linux command line experience. It is purposely decoupled from the host system so that it can run on any Linux system.  

`bluefin-cli` comes preconfigured with the [Homebrew](https://brew.sh/) package manager and comes ready to go out of the box. It is the current recommended method to install command line applications in Bluefin.
- System level commands that are not in the container such as `rpm-ostree`, `podman`, `docker`, `systemctl`, and `ujust` transparently work. Commands that require `sudo` on the host will not work, use the host terminal in Ptyxis for those use cases. 
-  The `brew` command works as it does on other operating systems.
- This [introductory video](https://www.youtube.com/watch?v=to3WAHLd_RA) goes over the features and history of Wolfi, which is designed for running in containers. 
- We feel that a distroless approach to deliver the entirety of the Homebrew ecosystem in a container is the perfect compliment to an existing host operating system. 

> **Note**: We do not recommend installing Homebrew on the host as this can lead to conflicting libraries between brew and the system. 

#### Included software

`bluefin-cli` comes with the latest versions of `bash`, `fish`, and `zsh` included, as well as some other fantastic command line tools:
- [atuin](https://github.com/atuinsh/atuin) for shell history
- [eza](https://github.com/eza-community/eza) as a replacement `ls`
- [fd](https://github.com/sharkdp/fd) for `find`
- [fzf](https://github.com/junegunn/fzf) for command line fuzzy finding
- [ripgrep](https://github.com/BurntSushi/ripgrep) for search
- [uutils](https://github.com/uutils/coreutils) as `coreutils`
- [zoxide](https://github.com/ajeetdsouza/zoxide) as `cd`

The entire container is rebuilt every day from scratch, and Wolfi's aggresive update policy ensures that Bluefin is always on the latest version of software. _Fully automated_. 

Brew's state is volume mounted to a file in your home directory so your container is fresh but your additional packages remain untouched. At this time it is **strongly recommended** to maintain a backup of your brew package list via the [brew bundle](https://docs.brew.sh/Manpage#bundle-subcommand) subcommand.  

The apk package manager is preferred for fully declarative setups with [boxkit](https://github.com/ublue-os/boxkit) or locally. You can file package requests on the [WolfiOS repository](https://github.com/wolfi-dev/) for packages that you may need.

The intended endstate of `bluefin-cli` is a fully automated declarative config managed via git using Wolfi packages for clean daily rebuilds. `brew` is used to fill out the "long tail" of existing software.

#### Use `bluefin-cli` on any Linux

`bluefin-cli` is for everyone! Here's the [distrobox](https://distrobox.it/) command.

    distrobox create -i ghcr.io/ublue-os/bluefin-cli -n bluefin

It'll work with any terminal, but is probably enjoyed to it's fullest with [Ptyxis](https://gitlab.gnome.org/chergert/ptyxis). If you're not on a Bluefin host we recommend [grabbing the quadlets](https://github.com/ublue-os/toolboxes) to get a managed, auto-updating experience. 

### Why a new container instead of just using Ubuntu or Fedora?

Alpha and Beta versions of Bluefin included Ubuntu as the default terminal experience. However, the team desired a distrobox that was designed from the bottom up to be a terminal experience instead of a traditional distribution. This is the way.   

[WolfiOS](https://github.com/wolfi-dev) was chosen due to:
- [These technical features](https://github.com/wolfi-dev#wolfi-features)
- The team's investment in tooling and automation
- Aggressive update cadence
- Packaging priorities strongly skew towards the tools our target audience wants.

> **Note**: Ubuntu and Fedora containers will always be included and receive the same optimizations such as instant-launch, Ptyxis integration, etc.

#### Assembling custom containers (Optional)

For specific projects we recommend _assembling_ on-demand distroboxes so that they are built fresh from scratch. Use the `ujust assemble` shortcut to declaratively build distroboxes defined in `/etc/distrobox/distrobox.ini`. This command will **destroy** your existing container and pull a new one from scratch. 

Modify `/etc/distrobox/distrobox.ini` to add your custom packages to the stock containers so that your preferred environment can be rebuilt. Check out [Declaring your own personal distroboxes](https://www.ypsidanger.com/declaring-your-own-personal-distroboxes/) for more information. Here's [an example distrobox.ini file](https://github.com/ublue-os/bluefin/blob/1ae2f3094cfaf5a581a89a440a2cb77507a9dcda/usr/etc/distrobox/distrobox.ini)

- Refer to the [Distrobox documentation](https://distrobox.privatedns.org/#distrobox) for more information on using and configuring custom images