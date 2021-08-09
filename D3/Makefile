run:
	sudo docker build -t jiahong/lp-jupyter:D3 -f Dockerfile .

	sudo docker run -dit --name jupyter-container --mount type=bind,source=/home/jiahong/liveProject/Real-time-Anomaly-Detection,target=/src  -p 8080:8888  jiahong/lp-jupyter:D3