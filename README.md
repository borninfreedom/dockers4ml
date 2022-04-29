**A collection of dockfiles for machine learning.**

- [darknet](https://github.com/borninfreedom/dockers4ml/tree/main/darknet)

**Some tips for using docker**

* Clear unused mirrors
```bash
sudo docker rmi $(sudo docker images -q)
sudo docker rm -v $(sudo docker ps -qa)
```

* Delete all docker images
```bash
sudo docker rmi -f $(sudo docker images -aq)
```

* Delete all docker images with there volumes
```bash
sudo docker rm -vf $(sudo docker ps -aq)
```

* Clean docker system
```bash
sudo docker system prune -a
```