# Использование PyTorch образа с поддержкой CUDA и cuDNN в качестве базового
FROM pytorch/pytorch:latest

# Set environment variables
ARG REDIS_HOST
ENV REDIS_HOST=$REDIS_HOST
ARG REDIS_PASSWORD
ENV REDIS_PASSWORD=$REDIS_PASSWORD

# Set CUDA environment variables
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility

# Обновление pip
RUN pip install --upgrade pip

RUN apt-get update && apt-get install -y \
    wget \
    make \
    gcc \
    procps \
    lsof \
    vim \
    supervisor  

WORKDIR /solution

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY /dev_parallel/ .

# Копируйте файл конфигурации supervisord в контейнер
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Используйте CMD для запуска supervisord
CMD ["/usr/bin/supervisord"]
