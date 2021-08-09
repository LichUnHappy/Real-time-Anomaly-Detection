# Real-time-Anomaly-Detection
Are you crazy? Or the network is crazy?

## D1 
build container with Dockerfile
```
cd D1
sudo docker build -t jiahong/lp-jupyter -f Dockerfile .
```

create and mount container to local host
```
sudo docker run -dit \
--name jupyter-container \
--mount type=bind,source=/home/jiahong/liveProject/Real-time-Anomaly-Detection,target=/src \
-p 8080:8888 \
jiahong/lp-jupyter
```

check the token
```
sudo docker exec -it <container> bash
```

## D2
build container with Dockerfile
```
cd D2
sudo docker build -t jiahong/lp-jupyter:D2 -f Dockerfile .
```

create and mount container to local host
```
sudo docker run -dit \
--name jupyter-container \
--mount type=bind,source=/home/jiahong/liveProject/Real-time-Anomaly-Detection,target=/src \
-p 8080:8888 \
jiahong/lp-jupyter:D2
```

## D3