FROM nvidia/cuda:11.8.0-base-ubuntu22.04

ENV PYTHONUNBUFFERED=1 

# system
# python3
RUN apt update -y -q && DEBIAN_FRONTEND=noninteractive apt install -y -q --no-install-recommends \
    software-properties-common apt-utils \
    curl git vim python3-dev g++ build-essential \
    python3.10 pip libgl1-mesa-dev ffmpeg \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && rm -rf /var/lib/apt/lists/*

# git
RUN git clone https://github.com/Plachtaa/VALL-E-X.git /VALL-E-X
RUN mkdir /VALL-E-X/checkpoints && mkdir /VALL-E-X/whisper && mkdir /huggingface && cd /huggingface && \
curl -L https://huggingface.co/Plachta/VALL-E-X/resolve/main/vallex-checkpoint.pt > vallex-checkpoint.pt && \
curl -L https://openaipublic.azureedge.net/main/whisper/models/345ae4da62f9b3d59415adc60127b97c714f32e89e936602e85993674d08dcb1/medium.pt > medium.pt && \
cp -p ./vallex-checkpoint.pt /VALL-E-X/checkpoints/. && \
cp -p ./medium.pt /VALL-E-X/whisper/. && \
rm -r -f /huggingface
WORKDIR /VALL-E-X

# requirements pytorch
RUN pip install -r requirements.txt

# shell
ENTRYPOINT ["python3", "launch-ui.py"]
