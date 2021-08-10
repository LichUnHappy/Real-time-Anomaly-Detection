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

To show the token, first exec into the container
```
sudo docker exec -it <container> bash
```
Then,
```
jupyter notebook list
```

## D3
use Makefile to build and run docker

Makefile looks like:
```
run:
    sudo docker build xxx
    sudo docker run xxx
```

Enter the $pwd and run
```
make run
```

Persistant storage of the trained weights
```
from joblib import dump, load
dump(clf, 'filename.joblib')
```
load the weights
```
clf = load('filename.joblib')
```

Connect 2 matrxi by coloum -> np.c_
```
a = np.array([[1, 2, 3], [7, 8, 9]])
b = np.arry([[4, 5, 6], [8, 8, 8]])
c = np.c_[a, b]
```

To draw the decision frontier, enough sample points as the background layer and trained classfier are required. The workflow is first generate dense enough sample points and punch them through the classfier and color them by the classification result.
```
# set the figure size
plt.rcParams['figure.figsize'] = [15, 15]
# generate dense enough sample points
xx, yy = np.meshgrid(np.linspace(-2, 70, 100), np.linspace(-2, 70, 100))
# punch the sample points through the classfier
Z = clf.decision_function(np.c_[xx.ravel(), yy.ravel()])
Z = Z.reshape(xx.shape)

# 等高线
plt.contourf(xx, yy, Z, levels=np.linspace(Z.min(), 0, 8), cmap=plt.cm.PuBu, alpha=0.5)
plt.contour(xx, yy, Z, levels=[0], linewidths=2, colors='g')
```

# D4
Got fastapi template.

check the current logs in the container
```
sudo docker logs <container>
```

# D5
Old friend.

Problem: ERROR: Couldn't connect to Docker daemon at http+docker://localhost - is it running?
```
sudo usermod -aG docker $USER
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo service docker restart
```

Caddy: Panic! casued by Ubutnu 20.04 LTS's resolv.conf. Pass the modified resolv.conf to caddy instance. The modified file is like following:
```
nameserver 127.0.0.11
options edns0 ndots:0
search internet-only.domain
```

# D6

Rebuild the fastapt imgae  with metrics. Update the requirements.txt and rebuid it with makefile:
```
run:
	sudo docker build -t jiahong/lp-fastapi:D6 -f Dockerfile .
```

Stop the current docker-compose
```
docker-compose down -v
```

Cannot access the prometheus in the grafana container. The solution is to replace the ip address in host network by the ip in docker network
```
docker inspect <prometheus container>
```
