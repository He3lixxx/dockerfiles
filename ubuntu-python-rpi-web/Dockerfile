FROM ubuntu:14.04
VOLUME /workspace
WORKDIR /workspace
MAINTAINER openHPI team <openhpi-info@hpi.de>
RUN apt-get update && apt-get install -y make Xfvb python3-pip firefox
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV PYTHONPATH $PYTHONPATH:/usr/lib/python3.4:/workspace
ENV PATH $PATH:/usr/lib/python3.4

# Start virtual display server
RUN Xvfb :99 &

# Get geckodriver
RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.17.0/geckodriver-v0.17.0-linux64.tar.gz
RUN tar xfvz geckodriver-v0.17.0-linux64.tar.gz
RUN mv geckodriver /usr/local/bin
RUN rm geckodriver-v0.17.0-linux64.tar.gz geckodriver

RUN adduser --disabled-password --gecos Python python
USER python

# Set up selenium venv for the test
RUN mkdir test
RUN virtualenv test/venv
RUN . test/venv/bin/activate
RUN pip3 install selenium
RUN deactivate

# Set up flask venv for the server
RUN mkdir server
RUN virtualenv server/venv
RUN . server/venv/bin/activate
RUN pip3 install flask
RUN deactivate
