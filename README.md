# docker-healess

By `XRDP/NOVNC` with `XFCE4` based on `Debian`, Formatting a HeadlessBox/Cloud Desktop.

- Screen shared with both RDP/noVnc. (ReadWrite/ReadOnly)
- MultiScreen support. (mstsc+xrdp+tigervnc)
- Audio support. (xrdp+pulseaudio)
- Locale/TZ support.
- Desktop apps: ibus-rime, flameshot, PAC.

**QuickStart**

```bash
# example1: quickStart
docker run -it --rm --shm-size 1g --net=host infrastlabs/docker-headless:full

# example2: VNC_RW=ChangeMe, VNC_RO=View123
# Caution: Please change the SSHPass when the Box started!!!
vols="""
-v /_ext:/_ext 
-v /opt:/opt 
-v /var/run/docker.sock:/var/run/docker.sock
"""
docker run -d --name=devbox --privileged --shm-size 1g --net=host \
 -e L=zh_CN -e VNC_RW=ChangeMe -e VNC_RO=View123 $vols infrastlabs/docker-headless:full

# 290.545 MB
docker container update --restart=always devbox
```

**Detail**

- Size: latest: `168.347 MB`, slim: `88.929 MB`, full: `289.581 MB`
- User: `headless`, SSHPass: `headless`, VNCPass: `headless`
- Ports
  - novnc 6080 > 10081
  - xrdp  3389 > 10089
  - sshd  22   > 10022
- HotKeys `super: Alt`
  - `sup+t`: terminal
  - `sup+f`: thunar
  - `sup+d`: rofi
  - `sup+q`: flameshot
  - `sup+h` : hide window
  - `sup+up`: max window
  - `sup+down`: cycle windows
  - `sup+left`: left workspace
  - `sup+right`: right workspace
- Entry: xrdp, novnc, dropbear
- 命令工具：`tree htop gawk expect tmux rsync iproute2`
- 图形工具：`sakura tint2 plank flameshot`, `gnome-system-monitor engrampa ristretto`
- tzdata时区, ttf-wqy-microhei字体, ibus-rime输入法,
- oh-my-bash, docker-dind

**Refs**

- https://github.com/accetto/xubuntu-vnc-novnc #276.52 MB
- https://github.com/hectorm/docker-xubuntu #633.29 MB
- https://github.com/ConSol/docker-headless-vnc-container
- https://github.com/jlesage/docker-firefox
- https://github.com/fadams/docker-gui #book
- https://hub.fastgit.org/aerokube/selenoid
- https://github.com/frxyt/docker-xrdp #DE
