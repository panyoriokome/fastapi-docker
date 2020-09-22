# 概要

Dockerを使わずにUvicornとGunicornを組み合わせて起動

## Setup

```
pip install requirements.txt
```


## Uvicornのみ

### サーバの立ち上げ

```
% uvicorn main:app --reload 
```

### 稼働確認

```
% curl "localhost:8000/items/15?q=sample"
{"item_id":15,"q":"sample"}
```

## Gunicorn + Uvicorn

### サーバの立ち上げ

```
% gunicorn main:app -w 4 -k uvicorn.workers.UvicornWorker -c config/gunicorn_settings.py
```

### 稼働確認

```
% curl "localhost:5000/items/15?q=sample"
{"item_id":15,"q":"sample"}

# Uvicornのデフォルトポートでアクセスできないことを確認
% curl "localhost:8000/items/15?q=sample"
curl: (7) Failed to connect to localhost port 8000: Connection refused
```