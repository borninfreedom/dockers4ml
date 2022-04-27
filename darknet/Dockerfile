#使用nvidia提供的cuda和cudnn环境作为基础镜像，devel分支可以正常使用nvcc等指令，一些依赖的编译需要nvcc。
FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04

#此命令可以指令镜像构建过程中使用的shell，默认是sh，因此改为常用的bash。
SHELL ["/bin/bash","-c"]

COPY ./sources.list /

RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak && cp /sources.list /etc/apt/

RUN apt update && DEBIAN_FRONTEND=noninteractive TZ=Asia/Shanghai apt-get -y install tzdata \
python3 \
python3-pip \
swig \
git \
vim \
tree \
cmake \
g++ \
gcc \
libopencv-dev

RUN apt update && apt install -y openssh-server && \
rm -rf /var/lib/apt/lists/*

RUN mkdir /var/run/sshd && \
echo 'root:root' | chpasswd && \
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
sed -i 's/\/usr\/lib\/openssh\/sftp-server/internal-sftp/' /etc/ssh/sshd_config

EXPOSE 22

WORKDIR /

COPY ./darknet /darknet

RUN cd /darknet && \
sed -i 's/GPU=0/GPU=1/' Makefile && \
sed -i 's/OPENCV=0/OPENCV=1/' Makefile && \
make

RUN systemctl enable ssh && service ssh restart









