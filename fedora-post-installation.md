##### Add user to wheel group (sudo)

>su -c 'usermod -aG wheels yourusername'

##### Make necessary changes to dnf.conf - fastestmirror to choose the fastest mirror and deltarpm for saving some bandwidth and data

>sudo vi /etc/dnf/dnf.conf

>[main]\
>gpgcheck=1\
>installonly_limit=3\
>clean_requirements_on_remove=True\
>best=False\
>skip_if_unavailable=True\
>fastestmirror=true\
>deltarpm=true

##### Update repos and update your system
>sudo dnf update

##### Install necessary packages
>sudo dnf install neovim kernel-devel glances sysstat htop -y

##### Removing and disabling useless things like bolt for thunderbolt which my system doesn't have, abrt for bug reports, fwupd used to update UEFI fimware - unsupported, and gnome-software which is a big fat useless blob

>sudo sh -c 'systemctl disable bolt && systemctl mask bolt'

>sudo dnf remove abrt fwupd gnome-software PackageKit* -y

##### Enabling ssh service

>sudo sh -c 'systemctl enable sshd && systemctl start sshd'

##### Adding [UnitedRPMs][urpm] repo since drivers in [RPMFusion][rfusion] repo for BCM4312 didn't work for me.

>sudo rpm --import https://raw.githubusercontent.com/UnitedRPMs/unitedrpms/master/URPMS-GPG-PUBLICKEY-Fedora

>sudo dnf -y install https://github.com/UnitedRPMs/unitedrpms/releases/download/15/unitedrpms-$(rpm -E %fedora)-15.fc$(rpm -E %fedora).noarch.rpm

>sudo dnf update --refresh

>sudo dnf -y groupinstall "Development Tools" 

>sudo dnf install broadcom-wl-dkms -y

##### Installing multimedia codecs
>sudo dnf install libva-utils gstreamer1-{vaapi,libav,plugins-{good,ugly,bad{-free,-nonfree}}} --setopt=strict=0

##### Installing Opera, VLC, qBittorent, Gnome Tweaks, and unizip/p7zip
>sudo dnf install vlc opera qbittorrent unzip p7zip gnome-tweaks -y

##### Performance Tweaks
>sudo sh -c 'dnf copr enable equeim/ananicy && dnf install ananicy -y && systemctl enable ananicy'

>sudo sh -c 'dnf install irqbalance -y && systemctl enable irqbalance'

>echo 'blacklist 'iTCO_wdt' | sudo tee /etc/modprobe.d/nowatchdog.conf

>sudo sh -c 'dnf install powertop -y && systemctl enable powertop'

##### Cosmetic Changes to boot splash
>plymouth-set-default-theme --list && sudo plymouth-set-default-theme text -R

[urpm]:https://github.com/UnitedRPMs/unitedrpms
[rfusion]:https://rpmfusion.org/
