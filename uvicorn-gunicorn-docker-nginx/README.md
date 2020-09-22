# 概要
FastAPIの公式でも紹介されているUvicornとGunicornが入ったチューニング済のDockerイメージを使った構築

[tiangolo/uvicorn-gunicorn-docker](https://github.com/tiangolo/uvicorn-gunicorn-docker)

## Setup

```
% docker build -t myimage .
% docker run -d --name mycontainer -p 80:80 myimage
```

## 稼働確認

```
% curl localhost/items/15
{"item_id":15,"q":null}% 
```