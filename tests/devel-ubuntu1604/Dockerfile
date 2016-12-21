FROM ubuntu:16.04
# You can change the FROM Instruction to your existing images if you like and build it with same tag
ENV container docker
ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive
RUN echo 'APT::Install-Recommends "0"; \n\
APT::Get::Assume-Yes "true"; \n\
APT::Get::force-yes "true"; \n\
APT::Install-Suggests "0";' > /etc/apt/apt.conf.d/01buildconfig
RUN mkdir -p  /etc/apt/sources.d/
RUN echo "deb mirror://mirrors.ubuntu.com/mirrors.txt xenial main restricted universe multiverse \n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-updates main restricted universe multiverse \n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-backports main restricted universe multiverse \n\
deb mirror://mirrors.ubuntu.com/mirrors.txt xenial-security main restricted universe multiverse" > /etc/apt/sources.d/ubuntu-mirrors.list
RUN apt-get update && apt-get install systemd sudo && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN cd /lib/systemd/system/sysinit.target.wants/; ls | grep -v systemd-tmpfiles-setup | xargs rm -f $1 \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*; \
rm -f /lib/systemd/system/plymouth*; \
rm -f /lib/systemd/system/systemd-update-utmp*;
RUN systemctl set-default multi-user.target

#
RUN \
  sed -i -e 's/^Defaults.*requiretty/Defaults    !requiretty/' -e 's/^%wheel.*ALL$/%wheel    ALL=(ALL)    NOPASSWD: ALL/' /etc/sudoers && \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget python-pip tree && \
  apt-get install -y libyaml-dev python-dev python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools && \
  apt-get install -y libffi-dev libssl-dev iproute2 && \
  pip install pyrax pysphere boto passlib dnspython

RUN mkdir /etc/ansible/
RUN echo -e '[local]\nlocalhost' > /etc/ansible/hosts
RUN pip install ansible

ENV init /lib/systemd/systemd
VOLUME [ "/sys/fs/cgroup" ]
# docker run -it --privileged=true -v /sys/fs/cgroup:/sys/fs/cgroup:ro 444c127c995b /lib/systemd/systemd systemd.unit=emergency.service
ENTRYPOINT ["/lib/systemd/systemd"]
CMD ["/bin/bash"]
