FROM python:3.9-alpine

RUN apk add --no-cache git

WORKDIR /app

RUN git clone https://github.com/rwv/chinese-dos-games-web.git . && \
    git submodule update --init --recursive --remote

RUN pip3 install --no-cache-dir flask

RUN sed -i 's/debug=True/host="0.0.0.0", port=5000, debug=True/g' app.py

# 创建到config目录的符号链接
RUN mkdir -p /config/dos-games && \
    ln -sf /config/dos-games /app/static/games/data

EXPOSE 5000

CMD ["python3", "app.py"]
