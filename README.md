# OPENSUSE-CUSTOM-SETUP
One more way to customize opensuse

## Working with software

### Repository list configuration

> Make sure the local repository of the installation stick is turned off.
> Add the Nvidia and Pacman repositories.
> You can do this through YaST.

### Adding a flathub repository

Flathub is used further to install some programs.

```sh
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### Uninstalling software

Some of the out-of-the-box software I never needed. So, I just delete it.

```sh
sudo zypper remove gnome-contacts gnome-weather gnome-maps cheese totem evolution gnome-chess quadrapassel polari swell-foop gnome-mahjongg gnome-sudoku gnome-mines lightsoff iagno gnome-extensions yelp
```

### Basic software installation

This is the base.

```sh
sudo zypper install git wget curl inxi neovim neofetch java-21-openjdk python311 python311-pip dkms gcc-c++
sudo systemctl enable dkms.service
```

Choose the latest version of java
```sh
sudo update-alternatives --config java
```

### NVIDIA graphics card driver installation

When installing drivers, it is very important to keep an eye on CPU load.

```sh
sudo zypper install nvidia-driver-G06-kmp-default nvidia-drivers-G06 nvidia-gl-G06 nvidia-gl-G06-32bit nvidia-utils-G06 nvidia-video-G06 nvidia-video-G06-32bit nvidia-compute-G06 nvidia-compute-G06-32bit 
```

### Basic software installation

This is the base.

```sh
sudo zypper install gitg gparted inkscape krita steam torbrowser-launcher vlc gnome-font-viewer
```

### Virt-manager installation

One of the best virtual machine managers.

```sh
sudo zypper install qemu-kvm bridge-utils virt-manager virt-top libguestfs guestfs-tools virt-install libvirt-devel libvirt
```

Add the user to a new group.

```sh
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

### Flatpak application installation

A huge suite of software for work and play.

```sh
flatpak install flathub com.github.tchx84.Flatseal org.kde.kdenlive org.onlyoffice.desktopeditors com.orama_interactive.Pixelorama com.github.Matoking.protontricks io.github.fabrialberio.pinapp com.github.GradienceTeam.Gradience com.vscodium.codium io.github.spacingbat3.webcord io.github.realmazharhussain.GdmSettings com.mattjakeman.ExtensionManager com.vysp3r.ProtonPlus com.heroicgameslauncher.hgl
```

## System customization

```
wget https://github.com/lassekongo83/adw-gtk3/releases/download/v5.1/adw-gtk3v5-1.tar.xz

sudo mv adw-gtk3 /usr/share/themes/adw-gtk3 
sudo mv adw-gtk3-dark /usr/share/themes/adw-gtk3-dark

flatpak install org.gtk.Gtk3theme.adw-gtk3 org.gtk.Gtk3theme.adw-gtk3-dark
```

```sh
git clone https://github.com/vinceliuice/Tela-circle-icon-theme.git
cd Tela-circle-icon-theme/
sudo ./install.sh standard
```
