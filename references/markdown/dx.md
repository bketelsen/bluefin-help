Bluefin Developer Experience (`bluefin-dx`) is a dedicated developer image with bundled tools. Unlike traditional Linux systems, the operating system and developer environment are explicitly and purposely separated. 

This means that tooling is not installed on the host, and is instead containerized, in a virtual machine, or scoped to the user's home directory. It is designed to meet the following use cases:

- Endeavors to be the world's most powerful [cloud native developer environment](https://landscape.cncf.io/)
- Full virtualization support
- Provide fleet management of Bluefin and other Linux systems via [Cockpit](https://cockpit-project.org/) (Incomplete, needs a volunteer!)

## The Cloud Native Approach

Bluefin goes "all in" on cloud native development and is used differently than a traditional distribution such as Ubuntu:

- GUI apps are installed via Flatpak
- Development is done in [devcontainers](https://containers.dev/)
- Command line applications are installed using [homebrew](https://brew.sh)
- Preconfigured ad-hoc containers for Ubuntu, Fedora, Wolfi, and a custom `bluefin-cli` container. Use whichever distribution you want. 

We strive to remove host level package management completely and consider these components as seperate layers. Communication between components is typically done via Flatpak Portals or via the container runtime. 

> This differs from apt, snap, and dnf where one packaging system handles both the graphical applications AND the command line applications.  This decoupling is what provides greater system reliability, near unlimited choice of software, and "distributed by default" development.  

In short, we picked it because this pattern is how servers are deployed in modern infrastructure. And the developers deploying those systems are already using homebrew and we want to leverage as much of that success as possible for the Linux desktop.

## Introduction

The pattern in `bluefin-dx` is centered around container focused development using [devcontainers](https://containers.dev).  Since development is not dependent on the operating system image, you can use whatever you want, you do not need to use everything in here in order to be productive -- think of them as prepaved paths that you can choose to use.  

Dev Containers were chosen to facilitate distributed development, each project has a declarative environment that is intended to be start the user with a "best practice" cloud-native workflow out of the box. The [Ultimate Guide to Dev Containers](https://www.daytona.io/dotfiles/ultimate-guide-to-dev-containers) has a good write up of the advantages of using devcontainers.

Homebrew can also be used for installation of development tools. 

>**Note**: This is an opinionated developer workflow that [differs from Fedora's use of toolbox](https://docs.fedoraproject.org/en-US/fedora-silverblue/toolbox/).  Toolbox is included for people who prefer the upstream approach. 

## Instructions

Any Bluefin machine can turn on DX mode, ISOs are also provided for new installations.

### Clean Installation

## [**bluefin-dx-gts.iso**](https://download.projectbluefin.io/bluefin-dx-gts.iso) [(checksum)](https://download.projectbluefin.io/bluefin-dx-gts-CHECKSUM) 
Recommended for developers with AMD and Intel based GPUs (3.7GB, based on Fedora 38)  
## [**bluefin-dx-nvidia-gts.iso**](https://download.projectbluefin.io/bluefin-dx-nvidia-gts.iso) [(checksum)](https://download.projectbluefin.io/bluefin-dx-nvidia-gts-CHECKSUM)  
Recommended for developers with Nvidia GPUs (5.4GB, based on Fedora 38)  

- If you are an experienced user who is comfortable troubleshooting and contributing feedback use: [**bluefin-dx-latest.iso**](https://download.projectbluefin.io/bluefin-dx-latest.iso) [(checksum)](https://download.projectbluefin.io/bluefin-dx-latest-CHECKSUM) / [**bluefin-dx-nvidia-latest.iso**](https://download.projectbluefin.io/bluefin-dx-nvidia-latest.iso) [(checksum)](https://download.projectbluefin.io/bluefin-dx-nvidia-latest-CHECKSUM)  
### Enabling Developer Mode on an existing Bluefin installation 

You can rebase to `bluefin-dx` by using the following command:

**Step 1 of 2** - `ujust devmode` to enable or disable the dx mode, then reboot:

![image|587x231](upload://7QIynueGfdPL9TzPqaNfjvMxIup.png)


**Step 2 of 2** - `ujust dx-group` - to add your user account to the right groups. Then log out and back in. This step only needs to be done once. 

Like all Universal Blue images, switching is atomic, allowing for clean switching between modes depending on the use case.

## Features

### Quality of Life Improvements

- [Cockpit](https://cockpit-project.org/) for local and remote management
- A collection of well curated monospace fonts
- [Tailscale](https://universal-blue.discourse.group/docs?topic=290) for VPN
- [Just](https://github.com/casey/just) task runner for post-install automation tasks. Check out [our documentation](https://universal-blue.org/guide/just/) for more information on using and customizing just.
- `fish` and `zsh` available as optional shells, use `ujust fish` or `ujust zsh` and follow the prompts to configure them
### Visual Studio Code with Docker

[Visual Studio Code](https://code.visualstudio.com/) is included on the image as the default IDE. It comes with the [devcontainers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) already installed. It's the recommended developer experience, start here if you're new to containerized development! 

- [Dev Containers Documentation](https://code.visualstudio.com/docs/devcontainers/containers) - you can skip most of the installation instructions and go directly to [the tutorial](https://code.visualstudio.com/docs/devcontainers/tutorial#_install-the-extension)
- [Dev Containers Specification](https://containers.dev/) 
- [Beginner's Series to: Dev Containers](https://www.youtube.com/watch?v=b1RavPr_878) - great introductory tutorial from the [VS Code YouTube channel](https://www.youtube.com/@code/videos)

The most current [Docker Engine](https://docs.docker.com/engine/) is included by default and is set up to be the default container runtime for vscode. [DevPod](https://devpod.sh/docs/what-is-devpod) is included to use devcontainer functionality across clouds and self-hosted setups. 

- Follow [Quickstart VS Code](https://devpod.sh/docs/getting-started/quickstart-vscode) to set up the environment.
  
## Command Line Experience

Manage your containers with Ptyxis's built in container support: 

![image|537x375](upload://8zQ13uWjjidPRtjflQ3CoSZCCUu.png)

[Ptyxis](https://universal-blue.discourse.group/docs?topic=300) also includes a host terminal so that you can quickly switch between containers and the host. 

- Further instructions on using Ptyxis: https://universal-blue.discourse.group/docs?topic=300

## Other Tooling

### JetBrains

`ujust jetbrains-toolbox` will fetch and install the [JetBrains Toolbox](https://www.jetbrains.com/toolbox-app) application, which will manage the installation of the JetBrains set of tools. This application will handle installation, removal, and upgrade of the JetBrains products, and is handled completely in your home directory, independent of the operating system image.

Check the [Jetbrains documentation](https://www.jetbrains.com/help/idea/podman.html) for integrating those tools with the podman runtime. Also check out how to [setup Jetbrains with devcontainers](https://www.jetbrains.com/help/idea/connect-to-devcontainer.html)

- [Uninstallation instructions](https://toolbox-support.jetbrains.com/hc/en-us/articles/115001313270-How-to-uninstall-Toolbox-App-)

### Kubernetes and other Cloud Native Tooling

- [kind](https://kind.sigs.k8s.io/) - Run a Kubernetes cluster on your machine. Run `kind create cluster` on the host to get started!
  - [kubectl](https://kubernetes.io/docs/reference/kubectl/) - Administer Kubernetes Clusters
  - helm, ko, flux, minio-client -- if it's an incubated project we intend to add it where appropriate

### Virtualization and Container Runtimes

- [virt-manager](https://virt-manager.org/) and associated tooling (KVM, qemu)
- [Incus](https://linuxcontainers.org/incus/) provides system containers
  - [LXC](https://linuxcontainers.org/) and [LXD](https://ubuntu.com/lxd) are also provided for compatability reasons 

### Podman Development

All the upstream `podman` tools are included. This is the default system container runtime, and is the recommended developer configuration that Fedora ships with. 

- Install the [Podman Desktop application](https://flathub.org/apps/io.podman_desktop.PodmanDesktop) for graphical use. 

> Though `bluefin-dx` defaults to docker and vscode for development, all of the Fedora upstream tools are included for those that prefer that experience.