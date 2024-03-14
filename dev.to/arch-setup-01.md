## Introduction

At some point all of us wanted to have a fully customized and flexible Linux configuration, not having a pre-configured system like [Manjaro](https://manjaro.org/) for example. There must be people out there, who are not a big fans of **DE _([Desktop Environments](https://wiki.archlinux.org/title/desktop_environment))_**. Sure I also got into the arch world with [Plasma's KDE](https://wiki.archlinux.org/title/KDE), but after a while, it become dull, so that's when I started getting into configuring my setup, but when I had to do it every time I was reinstalling my operating system it became tiring, that's when I began to create a very customizable script stack.

## Golden mean
There is a fine line between having a complete self installing setup, or having a self configured installation. My goal was to have some scripts that helps me, but still kept the control in the user's hand.

This is done by using multiple smaller scripts which can install or configure different parts of the OS stack.

## Structure of a Linux GUI
It's important to understand, how a Linux is working before we start putting one together.

### Building blocks to have a GUI:
#### Display server (or window server)
This is the component which communicates directly with the kernel. It is the bridge between the OS kernel and its clients. The display servers have multiple **protocols** _(you can call them blueprints)_ to choose from. The most notable protocols:
##### X11
###### Server
The most known implementation of X11 is the [X.Org Server](https://en.wikipedia.org/wiki/X.Org_Server) or simply **X Server** or more simply **X**
The X server requires multiple parts to operate like a [Compositor](https://en.wikipedia.org/wiki/Compositing_window_manager) which makes the apps work off screen, in the background or over each other. The one that I am using here is the [Picom](https://wiki.archlinux.org/title/Picom) compositor.
###### Window manager
You'll also need a [window manager](https://wiki.archlinux.org/title/Window_manager) to have usable window system. It has two major types:
- [Stacking](https://wiki.archlinux.org/title/Window_manager#Stacking_window_managers) window managers, like the one in Windows
- [Tiling](https://wiki.archlinux.org/title/Window_manager#Tiling_window_managers) window managers, the most notable tiling window manager for X11 is [i3](https://wiki.archlinux.org/title/I3).

##### Wayland
Wayland is also a protocol, Wayland's protocol combines the [compositor](#x11) into the display server, hence they are called [Wayland compositors](https://wiki.archlinux.org/title/Wayland#Compositors). 
My favorite so far is [Hyprland](https://wiki.archlinux.org/title/Hyprland) which is a tiling window manager.

##### X11 vs Wayland
Since the X11 protocol is older then the Wayland protocol, hence the X server has bigger community behind it, then the Wayland compositors. 

#### Display managers
These are optional packages you can install to have visual login screen, but you can live perfectly fine without one. I personally don't like using one, because I like to switch between configuration, which is easier to start from the terminal.
Display manager is basically the login screen. Some of the favorites: [SDDM (X11 and Wayland)](https://wiki.archlinux.org/title/SDDM), [GDM (X11 and Wayland)](https://wiki.archlinux.org/title/GDM), [LightDM (X11)](https://wiki.archlinux.org/title/LightDM) 

## Capabilities

### Package collection installation
There is a script for easily installing packages from `<some-name>.conf` config files. These files are have to be under the `YOZORA_PATH/pkgs/` directory and must have the `.conf` extension.

With this you can use the `update` alias to install specific collections for use the `--all` flag to install all after each other.

For example:
```bash
update -l # Lists the available package collections
update <name> # Installes the given collection
update --all # Install all availabe collection
```
#### Extension packages
There is more optional packages available in the other parts of the yozora stack, like: `yozora-i3`, `yozora-polybar`, `yozora-hyprland`
You can follow this article series to learn more about those.

### Convenience aliases
#### bashrc
There are a lot of convenience aliases comes with the bashrc files:
```bash
bcr # the default for `brc --download` and pulls the latest versions of the bash files from the local yozora repo
bcr --upload # upload the files to the local repo, so that you can also version control your modifications
refresh # Sources the bash filse
```
#### Git

`gclone` is a powerful alias to clone repositories from custom hosts (*github is the default with ssh, and the logged in user*): `usage: gclone <repo> [user] [host] [is_ssh]`
`gl` is a [lazygit](https://github.com/jesseduffield/lazygit) extended command, fist refreshes the deleted remote branches and then opens lazygit.

#### Other tools

`dotnet_install` can easily install multiple dotner versions
## How to get started
### Disclaimer
These tools are currently only supports the Arch Linux package manager and Aur to install packages. The other non-package related scripts were written in bash, so those are distro independent

From the time you finished installing your OS, you can run:
```bash
git clone https://github.com/joshika39/yozora.git ~/.config/yozora && cd ~/.config/yozora

./shell/bash/updater.sh --download

source ~/.bashrc
```
## Contribution
If you found any mistake, that I wrote, please comment it so that I can fix it. Or you can find these articles in my [Github Repository](https://github.com/joshika39/literature/blob/main/dev.to/arch-setup-01.md)
