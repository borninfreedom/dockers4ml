# Build the docker image for darknet.
```bash
bash build.sh
```

# Run a container of the image.
```bash
sudo nvidia-docker run -it -p 8022:22 darknet:latest bash
```

# Use SSH
如果在启动container时，不指定命令，那么就会启动ssh服务，如果指定了命令，那么需要手动执行启动ssh服务的命令。

例如，使用如下指令启动container:
```bash
sudo nvidia-docker run -it -p 8022:22 --name darknet_latest  darknet:latest bash
```
这时候就会启动bash程序，而不会启动ssh服务，如果想使用ssh服务，需要在启动的container中手动执行`service ssh start`。

如果执行`sudo nvidia-docker run -d -p 8022:22 --name darknet_latest  darknet:latest`，

这时候就会自动启动ssh服务。

---

If you do not specify a command when starting the container, the SSH service will be started. 

If you specify a command, you need to manually execute the command to start the SSH service.

For example, use the following command to start a container:
```bash
sudo nvidia-docker run -it -p 8022:22 --name darknet_latest  darknet:latest bash
```
At this time, the bash program will be started instead of the SSH service. 

If you want to use the SSH service, you need to manually execute `service SSH start` in the started container.

If you run `sudo nvidia-docker run -d -p 8022:22 --name darknet_latest  darknet:latest`,
The SSH service will be started automatically at this time.

# Note
**If you are not in Chinese Mainland, please comment out the line 18 and the line 36 of the Dockerfile.**
The line 18 is:
```bash
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak && cp /sources.list /etc/apt/
```
The line 36 is:
```bash
RUN python3 -m pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```