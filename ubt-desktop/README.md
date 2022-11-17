# desktop

- Gnome: 基于Ubuntu官方版，找遍github只能在systemd下跑 (+elementaryos)
- Plasma: 基于Kubuntu 注：启动plasma需要privilege权限; cent7下跑不起来(Qt依赖库错误，kernel版本有关?)
- Cinna: 基于Mint, 无裁剪，欢迎页，有屏保锁屏
- Mate: 基于Mint, 无裁剪，欢迎页，有屏保锁屏
- Xfce4: 基于Mint, 清理Icon资源，集成Docky

SYS|TYPE|DE|WM
---|---|---|---
ubt2004|GShell|ele|gala/metacity
ubt2004|KShell|neon|kwin
ubt2004|Mint|mate|Marco
ubt2004|Mint|cinna|xx
ubt2004|Mint|xfce|xfwm
ubt2004|Box|flux|flux

## ele,neon

```bash
# gnome: ele > gala,wingpannel
- ele32: 
install-desktop-elementary.sh安装版2：
  dcp启动> su headless > gala & > io.ele.wingpanel > 手动调desk背景 #allOK

# ele debug
docker run -it --rm --net=host --shm-size 1g -e VNC_OFFSET=99   --tmpfs /run --tmpfs /run/lock --tmpfs /tmp -v /sys/fs/cgroup:/sys/fs/cgroup:rw   --cap-add SYS_BOOT --cap-add SYS_ADMIN -e START_SESSION="gnome-session --builtin --session=pantheon" infrastlabs/docker-headless:elementary

# sysd's start fail: headless下手动可启
export DISPLAY=:99
export HOME=/home/headless
export USER=headless
export SHELL=/bin/bash
export TERM=xterm
#setlocale> lang
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en

source /.env;  
export XDG_SESSION_TYPE=x11; export XKL_XMODMAP_DISABLE=1; 
unset SESSION_MANAGER; unset DBUS_SESSION_BUS_ADDRESS; 
exec dbus-launch --exit-with-session gnome-session --builtin --session=ubuntu |grep WARN #pantheon

```

- neon

```bash
# ==part2==============
#14 13.33 The following NEW packages will be installed:
#14 13.33   appstream apt-config-icons apt-config-icons-hidpi apt-config-icons-large
#14 13.33   apt-config-icons-large-hidpi cryfs encfs flatpak kde-config-gtk-style
#14 13.33   kde-config-gtk-style-preview kde-config-plymouth kde-config-screenlocker
#14 13.33   kde-config-sddm kde-config-updates kde-nomodeset kde-spectacle
#14 13.33   kde-style-oxygen-qt5 kdeconnect kdegraphics-thumbnailers
#14 13.33   kdeplasma-addons-data kpackagelauncherqml kpackagetool5 kpeople-vcard kross
#14 13.33   kwin-addons libappstream-glib8 libavahi-glib1 libblockdev-crypto2
#14 13.33   libbluetooth3 libcanberra-pulse libfakekey0 libflatpak0 libfwupd2 libjcat1
#14 13.33   libkcolorpicker0 libkf5contacts-data libkf5contacts5 libkf5i18nlocaledata5
#14 13.33   libkf5kdcraw5 libkf5kdelibs4support5-bin libkf5krosscore5 libkf5krossui5
#14 13.33   libkf5modemmanagerqt6 libkf5prisonscanner5 libkf5pulseaudioqt3
#14 13.33   libkf5purpose-bin libkf5purpose5 libkf5unitconversion-data
#14 13.33   libkf5unitconversion5 libkimageannotator-common libkimageannotator0
#14 13.33   libmalcontent-0-0 libmarkdown2 libmm-glib0 libndp0 libnewt0.52 libnm0
#14 13.33   libopenconnect5 libostree-1-1 liboxygenstyle5-5 liboxygenstyleconfig5-5
#14 13.33   libqca-qt5-2 libqca-qt5-2-plugins libqmobipocket2 libqt5quickparticles5
#14 13.33   libqt5script5 libqt5webengine5 libqt5webview5 libqt5xmlpatterns5 libraw19
#14 13.33   libsnapd-qt1 libstoken1 libteamdctl0 libtinyxml2-6a libtss2-esys0
#14 13.33   libvolume-key1 mobile-broadband-provider-info neon-adwaita neon-apport
#14 13.33   neon-configure-inotify neon-essentials-desktop neon-ubuntu-advantage-tools
#14 13.33   network-manager plasma-browser-integration plasma-calendar-addons
#14 13.33   plasma-dataengines-addons plasma-discover plasma-discover-backend-flatpak
#14 13.33   plasma-discover-backend-snap plasma-discover-common plasma-disks plasma-nm
#14 13.33   plasma-pa plasma-runners-addons plasma-vault plasma-wallpapers-addons
#14 13.33   plasma-widgets-addons pulseaudio-module-gsettings qml-module-org-kde-bluezqt
#14 13.33   qml-module-org-kde-breeze qml-module-org-kde-kaccounts
#14 13.33   qml-module-org-kde-kio qml-module-org-kde-people qml-module-org-kde-prison
#14 13.33   qml-module-org-kde-purpose qml-module-org-kde-runnermodel
#14 13.33   qml-module-qtquick-particles2 qml-module-qtquick-xmllistmodel
#14 13.33   qml-module-qtwebengine qml-module-ubuntu-onlineaccounts smartmontools sshfs
#14 13.33   tpm-udev xdg-dbus-proxy xsettingsd


#14 13.33 The following packages will be upgraded:
#14 13.33   libseccomp2
#14 17.44 1 upgraded, 115 newly installed, 3 to remove and 43 not upgraded.
#14 17.44 Need to get 21.4 MB of archives.
```

## 使用

```bash
# https://github.com/darkdragon-001/Dockerfile-Ubuntu-Gnome #ubt2004: fks 57, star 16
docker  run -it --rm -p 10081:10081 -p 10089:10089 \
  --tmpfs /run --tmpfs /run/lock --tmpfs /tmp \
  --cap-add SYS_BOOT --cap-add SYS_ADMIN \
  -v /sys/fs/cgroup:/sys/fs/cgroup \
infrastlabs/docker-headless:gnome

# plasma: 需要privileged 否则start_kdeinit: Operation not permitted
docker  run -it --rm -p 11081:10081 -p 11089:10089   --tmpfs /run --tmpfs /run/lock --tmpfs /tmp   --privileged   -v /sys/fs/cgroup:/sys/fs/cgroup infrastlabs/docker-headless:plasma
```

**TODO**

- gnome: ibus-daemon -drx; tray图标才出来

## 问题记录

- ele: gala
- neon: # --: lib err

```bash
# Plasma: cent7下跑不起来(Qt依赖库错误，kernel版本有关?)
#   PVE6.3-2; SUSE12环境下正常
[root@node191 desktop]# docker exec -it 70610f748a4d bash
root@70610f748a4d:/home/headless# startplasma-x11 
startplasma-x11: error while loading shared libraries: libQt5Core.so.5: cannot open shared object file: No such file or directory
root@70610f748a4d:/home/headless# su - headless
headless @ 70610f748a4d in ~ |12:21:55  
$ startplasma-x11
startplasma-x11: error while loading shared libraries: libQt5Core.so.5: cannot open shared object file: No such file or directory
```

**docky**

```bash
# 依赖大；容器下使用体验不好，延迟/卡顿(改用plank/xcompmgr)
# docky@ubt2004: https://blog.csdn.net/Nozidoali/article/details/119838043
RUN export DOMAIN="mirrors.ustc.edu.cn"; mkdir -p /tmp/docky/deps; cd /tmp/docky/deps; \
  wget http://archive.ubuntu.com/ubuntu/pool/main/g/glibc/multiarch-support_2.27-3ubuntu1_amd64.deb; \
  wget http://archive.ubuntu.com/ubuntu/pool/universe/libg/libgnome-keyring/libgnome-keyring-common_3.12.0-1build1_all.deb; \
  wget http://archive.ubuntu.com/ubuntu/pool/universe/libg/libgnome-keyring/libgnome-keyring0_3.12.0-1build1_amd64.deb; \
  wget http://archive.ubuntu.com/ubuntu/pool/universe/g/gnome-keyring-sharp/libgnome-keyring1.0-cil_1.0.0-5_amd64.deb; \
  wget http://archive.ubuntu.com/ubuntu/pool/universe/g/gnome-sharp2/libgconf2.0-cil_2.24.2-4_all.deb;
  # sudo apt-get install ./*.deb
RUN mkdir -p /tmp/docky; cd /tmp/docky; \
  wget http://archive.ubuntu.com/ubuntu/pool/universe/d/docky/docky_2.2.1.1-1_all.deb;
  # sudo apt-get install ./docky_2.2.1.1-1_all.deb
# docky deps: 14.6M #err-noPkg: libgconf2.0-cil libgnome-keyring1.0-cil  #nonSysd-run-err: DBus not find.
RUN apt.sh mono-runtime libdbus-glib2.0-cil libdbus2.0-cil libgkeyfile1.0-cil libglib2.0-cil libgtk2.0-cil \
  libmono-addins0.2-cil libmono-cairo4.0-cil libmono-corlib4.5-cil libmono-posix4.0-cil libmono-sharpzip4.84-cil libmono-system-core4.0-cil \
  libmono-system-web4.0-cil libmono-system-xml-linq4.0-cil libmono-system-xml4.0-cil libmono-system4.0-cil libnotify0.4-cil libwnck22 gconf2
# docky_2.2.0-2_all.deb	2013-11-19 19:03 	592K
# docky_2.2.1.1-1_all.deb	2015-09-03 09:23 	609K
# http://archive.ubuntu.com/ubuntu/pool/universe/d/docky/
RUN cd /tmp/docky/deps; apt -y install ./*.deb; \
  cd /tmp/docky; apt -y install ./docky_2.2.1.1-1_all.deb; \
  mkdir -p /home/headless/.config/autostart; \
  cp /usr/share/applications/docky.desktop /home/headless/.config/autostart/

```