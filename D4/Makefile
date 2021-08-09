run:
	sudo docker build -t jiahong/lp-fastapi:D4 -f Dockerfile .

	sudo docker run -dit --name jupyter-fastapi --mount type=bind,source=/home/jiahong/liveProject/Real-time-Anomaly-Detection,target=/app -p 8000:8000 jiahong/lp-fastapi:D4

