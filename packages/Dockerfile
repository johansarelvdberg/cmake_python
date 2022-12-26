FROM python:3.8-bullseye
WORKDIR /dir
RUN apt-get update
RUN apt-get upgrade -y
RUN pip install --upgrade pip
RUN pip install pip-download
# Launch built application
CMD  /bin/bash
