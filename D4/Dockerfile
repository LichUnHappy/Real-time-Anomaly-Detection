FROM python:3.7-slim

COPY requirements.txt /
COPY model.joblib /
COPY main.py /

RUN pip3 install -r requirements.txt

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]