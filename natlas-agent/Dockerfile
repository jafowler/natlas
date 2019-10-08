FROM ubuntu:18.04

ARG AQUATONEURL='https://github.com/michenriksen/aquatone/releases/download/v1.4.3/aquatone_linux_amd64_1.4.3.zip'

WORKDIR /natlas-agent

COPY . /natlas-agent

RUN apt-get -qq update

RUN apt-get -qqy install \
	python3.6 \
	python3-pip \
	virtualenv \
    nmap \
    chromium-browser \
    unzip \
    xvfb \
    vncsnapshot \
    wget 

RUN wget $AQUATONEURL -O /tmp/aquatone.zip -q && \
    unzip /tmp/aquatone.zip -d /tmp/aquatone && \
    cp /tmp/aquatone/aquatone /usr/local/bin/aquatone && \
	rm -rf /tmp/aquatone.zip /tmp/aquatone

RUN virtualenv -p /usr/bin/python3 /natlas-agent/venv

# This is the same as running "source /natlas-agent/venv/bin/activate"
RUN . /natlas-agent/venv/bin/activate && pip3 -q install --trusted-host pypi.python.org -r requirements.txt

CMD . /natlas-agent/venv/bin/activate && python3 natlas-agent.py