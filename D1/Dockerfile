FROM python:3.7-slim

RUN mkdir src 
WORKDIR /src

RUN pip3 install notebook

CMD ["jupyter", "notebook", "--port=8888", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
