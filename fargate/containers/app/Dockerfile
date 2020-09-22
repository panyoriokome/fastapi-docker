FROM python:3.7-slim AS test
LABEL application=textanalysis

RUN apt-get update
RUN apt-get install -y --no-install-recommends gcc g++ make

# Create app  group and user
RUN groupadd --gid 1000 app && \
    useradd -u 1000 -g app app

# Copy source code
COPY --chown=app:app . /app
WORKDIR /app

RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt --no-cache-dir --no-input

USER app

CMD [ "uwsgi", "--ini", "app.ini" ]