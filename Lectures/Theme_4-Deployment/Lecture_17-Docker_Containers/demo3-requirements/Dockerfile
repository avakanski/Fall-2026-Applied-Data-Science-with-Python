FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

RUN mkdir model
ENV MODEL_DIR=/app/model
ENV MODEL_FILE=model.joblib

COPY train.py ./train.py
COPY inference.py ./inference.py

RUN python train.py

CMD [ "python", "./inference.py"]
