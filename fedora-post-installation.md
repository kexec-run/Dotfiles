### Things to Do After Fresh Installation of Fedora


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
>sudo dnf upgrade

##### Install necessary packages
>sudo dnf in neovim kernel-devel -y

##### Removing and disabling useless things like bolt for thunderbolt which my system doesn't have, abrt for bug reports, fwupd used to update UEFI firmware - unsupported, and gnome-software which is a big fat useless blob

>sudo systemctl disable --now bolt

>sudo dnf remove abrt fwupd gnome-software PackageKit* -y

##### Enabling ssh service

>sudo systemctl enable --now sshd

##### Adding [UnitedRPMs][urpm] repo since drivers in [RPMFusion][rfusion] repo for BCM4312 didn't work for me.

>sudo rpm --import https://raw.githubusercontent.com/UnitedRPMs/unitedrpms/master/URPMS-GPG-PUBLICKEY-Fedora

>sudo dnf -y in https://github.com/UnitedRPMs/unitedrpms/releases/download/15/unitedrpms-$(rpm -E %fedora)-15.fc$(rpm -E %fedora).noarch.rpm

>sudo dnf update --refresh

>sudo dnf -y groupinstall "Development Tools" 

>sudo dnf in broadcom-wl-dkms -y

##### Installing multimedia codecs
>sudo dnf in libva-utils gstreamer1-{vaapi,libav,plugins-{good,ugly,bad{-free,-nonfree}}} --setopt=strict=0

##### Installing Essentials
>sudo dnf in vlc opera qbittorrent unzip p7zip p7zip-plugins gnome-tweaks gvfs-{fuse,mtp,nfs,smb} glances sysstat htop fuse-{exfat,sshfs} exfat-utils hexchat -y

##### Performance Tweaks
>sudo sh -c 'dnf copr enable equeim/ananicy && dnf in ananicy -y && systemctl enable --now ananicy'

>sudo sh -c 'dnf in irqbalance -y && systemctl enable --now irqbalance'

>echo 'blacklist 'iTCO_wdt' | sudo tee /etc/modprobe.d/nowatchdog.conf

>sudo sh -c 'dnf in powertop -y && systemctl enable --now powertop'

>sudo sh -c 'dnf in tuned -y && systemctl enable --now tuned && tuned-adm profile balanced'

##### Cosmetic Changes to boot splash
>plymouth-set-default-theme --list && sudo plymouth-set-default-theme text -R

##### Installing better fonts

>sudo  dnf copr enable dawid/better_fonts

>sudo dnf in fontconfig-enhanced-defaults fontconfig-font-replacements

[urpm]:https://github.com/UnitedRPMs/unitedrpms
[rfusion]:https://rpmfusion.org/
