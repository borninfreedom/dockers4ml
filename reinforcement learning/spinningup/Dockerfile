#使用nvidia提供的cuda和cudnn环境作为基础镜像，devel分支可以正常使用nvcc等指令，一些依赖的编译需要nvcc。
#The CUDA and cudnn environments provided by NVIDIA are used as the basic images. The devel branch 
#can normally use nvcc and other instructions. Nvcc is required for some dependent compilers
FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04

#此命令可以指令镜像构建过程中使用的shell，默认是sh，因此改为常用的bash。
#This command can instruct the shell used in the process of image construction. 
#The default is sh, so it is changed to bash.
SHELL ["/bin/bash","-c"]

COPY ./sources.list /
#替换为国内源
#Replace with the source of China.
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
libopencv-dev \
libopenmpi-dev


RUN python3 -m pip install -U pip

#设置国内源
#Set the Chinese pip source
#If you are not in Chinese Mainland, please comment out this line of code.
RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

RUN apt update && apt install -y openssh-server && \
rm -rf /var/lib/apt/lists/*

##配置SSH##
##Configure SSH##
RUN mkdir /var/run/sshd && \
#此处的'root:root'分别表示用户名和密码，此时给root用户设置的密码是root，在ssh登录时使用。可以修改为其他的密码。
#'root: root' here represents the user name and password respectively. At this time, the password set 
#for the root user is root, which is used during SSH login. It can be changed to other passwords.
echo 'root:root' | chpasswd && \
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
#修改此处才能让pycharm远程登录进来
#Modify here to allow pycharm to log in remotely.
sed -i 's/\/usr\/lib\/openssh\/sftp-server/internal-sftp/' /etc/ssh/sshd_config

EXPOSE 22

WORKDIR /


COPY ./spinningup /spinningup
RUN cd /spinningup && python3 -m pip install -e .


#如果在启动container时，不指定命令，那么就会启动ssh服务，如果指定了命令，那么需要手动执行启动ssh服务的命令
#例如，使用如下指令启动container
#sudo nvidia-docker run -it -p 8022:22 --name darknet_latest  darknet:latest bash
#这时候就会启动bash程序，而不会启动ssh服务，如果想使用ssh服务，需要在启动的container中手动执行service ssh start
#如果执行sudo nvidia-docker run -d -p 8022:22 --name darknet_latest  darknet:latest
#这时候就会自动启动ssh服务

#If you do not specify a command when starting the container, the SSH service will be started. 
#If you specify a command, you need to manually execute the command to start the SSH service.
#For example, use the following command to start a container
#sudo nvidia-docker run -it -p 8022:22 --name darknet_latest  darknet:latest bash
#At this time, the bash program will be started instead of the SSH service. If you 
#want to use the SSH service, you need to manually execute `service SSH start` in the started container.
#If you run `sudo nvidia-docker run -d -p 8022:22 --name darknet_latest  darknet:latest`,
#The SSH service will be started automatically at this time
CMD ["/usr/sbin/sshd","-D"]