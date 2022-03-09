FROM python:3.8-buster as builder

COPY Pipfile Pipfile.lock ./

RUN pip3 install pipenv && pipenv install --system

FROM python:3.8-slim-buster as runner

COPY --from=builder /usr/local/lib/python3.8/site-packages /usr/local/lib/python3.8/site-packages
COPY --from=builder /usr/local/bin/uwsgi /usr/local/bin/uwsgi

RUN apt update \
  && apt install -y libpq5 libxml2 procps vim curl \
  && apt clean \
  && rm -rf /var/lib/apt/lists/*

ENV APP_ROOT /home/uwsgi

WORKDIR $APP_ROOT

RUN useradd -m -s /bin/sh -u 1002 uwsgi

COPY . $APP_ROOT
RUN ln -nfs /usr/local $APP_ROOT/.venv

RUN mkdir /var/run/uwsgi
RUN chown -R uwsgi:uwsgi $APP_ROOT /var/run/uwsgi

USER uwsgi

ENTRYPOINT ["./docker-entrypoint.sh"]
