FROM python:3.10-alpine

RUN adduser -u 1000 -D app

RUN apk update && \
    apk add \
    pcre \
    pcre-dev \
    build-base \
    gcc \
    linux-headers \
    openssl \
    libffi-dev \
    && pip install pipenv

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile* /app/

RUN cd /app && pipenv install --system --deploy

COPY . /app

RUN chown -R app:app /app /var/www/app

USER app

WORKDIR /app

EXPOSE 5000

CMD flask --app . run --host=0.0.0.0 --port=5000