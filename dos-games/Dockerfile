FROM python:alpine3.16

LABEL maintainer="simkcy" \
      description="Chinese DOS Games for Home Assistant"

WORKDIR /app

# 使用国内镜像源加速下载
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk update && \
    apk add --no-cache git

# 克隆项目
RUN git clone https://github.com/rwv/chinese-dos-games-web.git /app && \
    cd /app && \
    git submodule update --init --recursive --remote

# 安装Python依赖
RUN pip3 install --no-cache-dir --upgrade pip && \
    pip3 install --no-cache-dir flask

# 配置修改和游戏数据下载
RUN cd /app && \
    sed -i "23,20583d" ./static/games/games.json && \
    python3 ./static/games/download_data.py && \
    sed -i 's/debug=True/host="0.0.0.0", port=5000, debug=True/g' ./app.py

# 创建数据目录
RUN mkdir -p /share/dos-games

EXPOSE 5000

CMD [ "python3", "/app/app.py" ]
