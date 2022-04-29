**A collection of dockfiles for machine learning.**

- [darknet](https://github.com/borninfreedom/dockers4ml/tree/main/darknet)
- [reinforcement learning](https://github.com/borninfreedom/dockers4ml/tree/main/reinforcement%20learning)
    - [spinningup](https://github.com/borninfreedom/dockers4ml/tree/main/reinforcement%20learning/spinningup)
    - [stable baseline3](https://github.com/borninfreedom/dockers4ml/tree/main/reinforcement%20learning/stable%20baselines3)
    - [rllib](https://github.com/borninfreedom/dockers4ml/tree/main/reinforcement%20learning/rllib)
    
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