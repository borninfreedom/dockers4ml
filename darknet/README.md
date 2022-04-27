# Build the docker image for darknet.
```bash
bash build.sh
```

# Run a container of the image.
```bash
sudo nvidia-docker run -it -p 8022:22 darknet:latest bash
```

# Use SSH
First, enter the container of the darknet:latest image, then run
```bash
service ssh start
```
Now you can ssh into the container through `ssh root@your-host-machine-ip -p 8022`。
