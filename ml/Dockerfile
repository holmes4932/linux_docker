FROM nvidia/cuda:11.6.1-cudnn8-devel-ubuntu20.04

ARG ML_USER

# install packages
RUN apt-get update
RUN yes | unminimize
RUN apt-get install -y tini iproute2 iputils-ping net-tools netcat
RUN apt-get install -y openssh-server sudo vim grep gawk rsync tmux man manpages manpages-dev manpages-posix manpages-posix-dev diffutils file
RUN apt-get install -y make python3 python3-pip python3-virtualenv
RUN apt-get install -y curl git zsh
RUN apt-get install -y byobu
# RUN apt-get install -y qemu-user-static gcc-mips64-linux-gnuabi64
# RUN apt-get install -y musl
# RUN ln -s /lib/x86_64-linux-musl/libc.so /usr/lib/libc.musl-x86_64.so.1

# install python packages
RUN pip3 install --upgrade pwntools
RUN pip3 install notebook

# /var/run/sshd: required on ubuntu
RUN mkdir /var/run/sshd

# locale
RUN apt-get install -y locales
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN /usr/sbin/locale-gen

# add user/group, empty password, allow sudo
RUN groupadd -g 1000 ${ML_USER}
RUN useradd --uid 1000 --gid 1000 --groups root,sudo,adm,users --create-home --password '' --shell /bin/bash ${ML_USER}
RUN echo '%sudo ALL=(ALL) ALL' >> /etc/sudoers

# gen ssh-keys, allow empty password
# RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
# RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
# RUN echo 'PermitEmptyPasswords yes' >> /etc/ssh/sshd_config
RUN echo 'StrictModes no' >> /etc/ssh/sshd_config
# RUN sed -i 's/nullok_secure/nullok/' /etc/pam.d/common-auth


# shell color
RUN echo 'export PS1="\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ "' >> /root/.bashrc
RUN echo 'export PS1="\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ "' >> /home/${ML_USER}/.bashrc

# run the service
EXPOSE 22
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["/usr/sbin/sshd", "-D"]



