# OPENSUSE-CUSTOM-SETUP
One more way to customize opensuse

## Working with software

### Repository list configuration

The community repository allows you to greatly expand the list of available software for the system.

> Make sure the local repository of the installation stick is turned off.
> Add the Nvidia and Pacman community repositories.
> You can do this through YaST.

### Uninstalling software

Some of the out-of-the-box software I never needed. So, I just delete it.

```sh
sudo zypper remove kontact kmahjongg kmines kreversi ksudoku akregator kaddressbook kmail kontact konversation ktnef knotes kpat libkdegames system-user-games libkdegames-lang mbox-importer-lang kdegames-carddecks-default kaddressbook-doc akonadi-contacts
```

### Installing useful software

Basic packages that we will need as we work with the system.

```sh
sudo zypper ref
sudo zypper dup

sudo zypper in git wget curl inxi opi zsh neovim fastfetch java-21-openjdk python311 python311-pip gcc-c++ clang aria2 dkms

# choose the latest version of java
sudo update-alternatives --config java
java --version

# load dkms daemon (need to reboot)
sudo systemctl enable dkms.service
systemctl status dkms.service
```

### NVIDIA graphics card driver installation

When installing drivers, it is very important to keep an eye on CPU load.

```sh
# open gnome-system-monitor and monitor CPU load
sudo zypper in nvidia-driver-G06-kmp-default nvidia-drivers-G06 nvidia-gl-G06 nvidia-gl-G06-32bit nvidia-utils-G06 nvidia-video-G06 nvidia-video-G06-32bit nvidia-compute-G06 nvidia-compute-G06-32bit
```

Reboot and check inxi

```sh
inxi -G
```

### Adding a flathub repository

Flathub is used further to install some programs.

```sh
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Basic software installation

This is the base.

```sh
sudo zypper in vlc steam krita inkscape torbrowser-launcher transmission-qt partitionmanager gamemode
```

### Virt-manager installation

One of the best virtual machine managers.

```sh
sudo zypper in qemu-kvm bridge-utils virt-manager libguestfs guestfs-tools virt-install libvirt-devel libvirt

sudo usermod -G libvirt -a <username>
```

Change the lines in qemu.conf with access to different functions.

> You have to change these lines:
> ```user = "<username>"```
> ```group = "libvirt"```

```sh
sudo nvim /etc/libvirt/qemu.conf
```

```sh
sudo systemctl enable libvirtd
```

### Enabling power safe tools

You can use tlp, or delete it and install power-profiles-daemon

> Use tlp

```sh
sudo systemctl enable tlp.service
```

> Use power-profiles-daemon

```sh
sudo systemctl disable tlp.service

# zypper will remove tlp
sudo zypper in power-profiles-daemon
```

### Flatpak application installation

A huge suite of software for work and play.

```sh
flatpak install flathub org.kde.kdenlive org.onlyoffice.desktopeditors com.orama_interactive.Pixelorama com.github.Matoking.protontricks com.vscodium.codium com.vysp3r.ProtonPlus com.heroicgameslauncher.hgl dev.vencord.Vesktop com.usebottles.bottles com.github.tchx84.Flatseal org.gtk.Gtk3theme.adw-gtk3-dark

sudo flatpak override com.vscodium.codium --env=GTK_THEME=adw-gtk3-dark
```

### Installing mod launcher for games (especially important for Risk Of Rain 2)

Native launcher for modding games.

> Download the latest release of the program
> https://github.com/ebkr/r2modmanPlus/releases

```sh
./<package_name>.AppImage
```

> Create desktop shortcut

```sh
nvim .local/share/applications/r2modman.desktop

# add it to the file
[Desktop Entry]
Name=R2modman
Comment=Infinite mod generator
Exec=/path/to/r2modman.AppImage --no-sandbox
Icon=fuse-emulator
Terminal=false
Type=Application
Categories=Game;
MimeType=x-scheme-handler/ror2mm;
```

### Installing the native engine for the game STALKER

Engine for the STALKER series of games. Makes the game native.

```sh
# download the necessary dependencies
sudo zypper in git cmake make gcc gcc-c++ glew-devel openal-devel cryptopp-devel libogg-devel libtheora-devel libvorbis-devel SDL2-devel lzo-devel libjpeg-turbo-devel

git clone https://github.com/OpenXRay/xray-16.git --recurse-submodules
cd xray-16 && mkdir bin && cd bin
cmake .. -DCMAKE_INSTALL_LIBDIR=lib64 -DCMAKE_INSTALL_PREFIX=/usr

# the number of cores is counted from zero
# if you have 4 cores, you should write 3
make -j<numberofcores>

QA_RPATHS=$(( 0x0001|0x0010 )) make package
sudo rpm -ivh <programname>
```

### Installing the open source version of the Minecraft Launcher

Launcher with open source code and convenient settings.

> Download the latest release of the program (we need a .jar version of the game) (! maybe to old !)
> https://tlaun.ch/jar
> Create desktop shortcut

```sh
nvim ~/.local/share/applications/Minecraft.desktop

# add it to the file
[Desktop Entry]
Name=Minecraft
Comment=Infinite idea generator
Exec=gamemoderun java -jar /path/to/LegacyLauncher_legacy.jar
Icon=minecraft
Terminal=false
Type=Application
Categories=Game;
```

### Installing a program for fan control on MSI notebooks

A system for managing special parameters on MSI laptops.

> Download the latest version of the software
> https://github.com/dmitry-s93/MControlCenter/releases/

```sh
sudo ./install.sh
```

### Clear system

```sh
sudo zypper packages --unneeded
# delete them using zypper
sudo zypper remove <package_name>

flatpak repair
flatpak uninstall --unused
```

## System customization

### Icon setup

> To make icons available to all users of the system, instead of ```./install.sh standard```, run ```sudo ./install.sh standard```.

```sh
# traditional icons
git clone https://github.com/vinceliuice/Tela-icon-theme.git
cd Tela-icon-theme
./install.sh standard

# rounded icons
git clone https://github.com/vinceliuice/Tela-circle-icon-theme.git
cd Tela-circle-icon-theme
./install.sh standard
```

> If you want to change some icons

```sh
sudo nvim .local/share/applications/com.github.Matoking.protontricks.desktop
sudo nvim .local/share/applications/com.orama_interactive.Pixelorama.desktop
sudo nvim .local/share/applications/dev.vencord.Vesktop.desktop
```

### ZSH installation and configuration

Install zsh and run it.

> Zsh will ask you to configure it after the first run.
> Look at all the items and click 0 in each if you are satisfied.

```sh
sudo zypper in zsh

# how to run
zsh
```

> This font supports icons.
> It is necessary for correct output of information in the terminal.

```sh
wget https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf

sudo mv MesloLGS\ NF\ Regular.ttf /usr/share/fonts/
```

### Oh-my-zsh framework

Oh-my-zsh will extend the capabilities of regular zsh.

```sh
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Plugins for zsh

These extensions will provide hints while using zsh.

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

> After installing the zsh extensions, you should put them in ```.zshrc```.
> Open the config and find the line ```plugins=(git)```.
> It should be changed to ```plugins=(git zsh-autosuggestions zsh-syntax-highlighting)```.

```sh
nvim .zshrc

plugins=(git zsh-autosuggestions zsh-syntax-highlighting)

# restart the config
source .zshrc
```

### P10K theme

P10k will make zsh more beautiful.

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

> After installing the 10k, you should put them in ```.zshrc```.
> You must replace the value of ZSH_THEME with ```ZSH_THEME="powerlevel10k/powerlevel10k"```.

```sh
nvim .zshrc

ZSH_THEME="powerlevel10k/powerlevel10k"

# restart the config
source .zshrc
```
