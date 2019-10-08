FROM ubuntu:18.04

ENV LC_ALL="C.UTF-8"
ENV LANG="C.UTF-8"

WORKDIR /natlas-server

COPY . /natlas-server

RUN apt-get -qq update && apt-get -qqy install curl sqlite3

RUN apt-get -qqy install \
	python3.6 \
	python3-pip \
	virtualenv

RUN virtualenv -p /usr/bin/python3 /natlas-server/venv

# This is the same as running "source /natlas-server/venv/bin/activate"
RUN . /natlas-server/venv/bin/activate && pip3 -q install --trusted-host pypi.python.org -r requirements.txt

EXPOSE 5000

CMD . /natlas-server/venv/bin/activate && flask db upgrade && /natlas-server/run-server.sh




