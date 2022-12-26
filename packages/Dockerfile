FROM python:3.8-bullseye
WORKDIR /dir
#RUN pip install --upgrade pip
RUN apt-get update
RUN apt-get upgrade -y
RUN pip install --upgrade pip
RUN pip install pip-download
# Launch built application
CMD  /bin/bash
#CMD pip download pypiserver;pip-download --show-config;pip-download -r requirements.txt