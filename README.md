# OPENSUSE-CUSTOM-SETUP
One more way to customize opensuse

## Working with software

```sh
sudo zypper remove gnome-contacts gnome-weather gnome-maps cheese totem evolution gnome-chess quadrapassel polari swell-foop gnome-mahjongg gnome-sudoku gnome-mines lightsoff iagno gnome-extensions yelp
```

```sh
sudo zypper install git wget curl inxi neovim neofetch java-21-openjdk python311 python311-pip dkms gcc-c++
sudo systemctl enable dkms.service
```

```sh
sudo zypper install nvidia-driver-G06-kmp-default nvidia-drivers-G06 nvidia-gl-G06 nvidia-gl-G06-32bit nvidia-utils-G06 nvidia-video-G06 nvidia-video-G06-32bit nvidia-compute-G06 nvidia-compute-G06-32bit 
```

```sh
sudo zypper install gitg gparted inkscape krita steam torbrowser-launcher vlc gnome-font-viewer
```

```sh
sudo zypper install qemu-kvm bridge-utils virt-manager virt-top libguestfs guestfs-tools virt-install libvirt-devel libvirt
sudo usermod -G libvirt -a <username>
sudo nvim /etc/libvirt/qemu.conf

sudo systemctl enable libvirtd
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
