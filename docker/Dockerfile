FROM python:3.11-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV YOLO_VERBOSE=False
ENV HYDRA_FULL_ERROR=1
ENV PYTHONPATH="${PYTHONPATH}:/app"

WORKDIR /app
RUN apt-get update && apt-get install -y wget vim gcc python3 python3-pip \
    && apt-get install -y libsm6 libxext6 git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 libgl1-mesa-glx

COPY requirements.txt .
RUN pip3 install --upgrade pip \
    && pip3 install -r requirements.txt

COPY . /app/ 

CMD ["python3", "main.py"]