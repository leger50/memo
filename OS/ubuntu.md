# Ubuntu - List of tools

First :
```
sudo apt update
sudo apt full-upgrade
```

## Standard developer tools

```
sudo apt install build-essential git
```

Gitkraken : https://support.gitkraken.com/how-to-install/

## Edition tools
### Visual Studio Code

Doc : https://code.visualstudio.com/docs/setup/linux
```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code # or code-insiders
```

### Gedit

Install & plugins :
```
sudo apt install gedit gedit-plugins
```
Themes :
- https://draculatheme.com/gedit

## Framework
### QTCreator

Install :
```shell
sudo apt install qtcreator
sudo apt install qt5-default #To configure qtcreator to use qt5
sudo apt install qt5-doc qt5-doc-html qtbase5-doc-html
```

Themes :
- https://github.com/foxoman/qDarkSky

## Multimedia tools
```
sudo apt install vlc ffmpeg flashplugin-installer
sudo apt install gthumb
sudo apt install libreoffice
sudo apt install gimp
```

## Networking tools

General :
```
sudo apt install libpcap-dev libnet1-dev rpcbind openssh-server nmap
sudo apt install wireshark
```

FTP :
```
sudo apt install filezilla
```

## Embedded Development

### General
```
sudo apt install minicom
```

### Buildroot

List of package requirement from : https://buildroot.org/downloads/manual/manual.html#requirement
```
sudo apt install patch gzip bzip2 perl cpio unzip rsync python
```

Optional packages to use an interface configuration :
```shell
sudo apt install libncurses5 libncurses-dev # To use the menuconfig interface
sudo apt install libglib2.0-dev libglade2-dev # To use the gconfig interface
# to use the xconfig interface, install qt5
```

### Yocto

List of package requirement from : https://www.yoctoproject.org/docs/latest/ref-manual/ref-manual.html#required-packages-for-the-host-development-system
```
sudo apt install python
sudo apt install gawk wget diffstat unzip texinfo gcc-multilib chrpath socat
sudo apt install autoconf automake libtool libglib2.0-dev
```

### Toolchain

- Linaro toolchain : https://www.linaro.org/downloads/ (exemple of toolchain : _gcc-linaro-7.5.0-2019.12-x86_64_arm-linux-gnueabihf_)

## Ubuntu tools
```
sudo apt install gnome-tweak-tool
sudo apt install psensor
```

## Others

Email
```
sudo apt install thunderbird thunderbird-locale-fr
```

Troubleshooting
```
sudo apt install teamviewer
```