FROM archlinux:base-20220807.0.72894

LABEL MAINTAINER="me@monlor.com"

ENV LANG='C.UTF-8' LANGUAGE='C:zh' LC_ALL='C.UTF-8' 
ENV TZ=Asia/Shanghai

ENV DUMB_INIT_VERSION="1.2.5"

# 加入中国镜像源和社区仓库
RUN curl -sL 'https://archlinux.org/mirrorlist/?country=CN&protocol=https&ip_version=4' \
        | sed 's/^#Server/Server/' > /etc/pacman.d/mirrorlist \
 && curl -sL 'https://raw.githubusercontent.com/archlinuxcn/mirrorlist-repo/master/archlinuxcn-mirrorlist' \
        | sed 's/^# Server/Server/' > /etc/pacman.d/archlinuxcn-mirrorlist \
 && echo '[archlinuxcn]' >> /etc/pacman.conf \
 && echo 'SigLevel = Optional TrustedOnly' >> /etc/pacman.conf \
 && echo 'Include = /etc/pacman.d/archlinuxcn-mirrorlist' >> /etc/pacman.conf \
 && pacman -Syy \
 # 更新pacman密钥
 && pacman-key --init \
 && pacman-key --populate archlinux \
 && pacman -S --noconfirm archlinuxcn-keyring \
 # dumb-init
 && curl -#fSLo /usr/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT_VERSION}/dumb-init_${DUMB_INIT_VERSION}_x86_64 \
 && chmod +x /usr/bin/dumb-init \
 # 设置中国时区
 && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 # 清理缓存
 && pacman --noconfirm -Scc

CMD /bin/bash