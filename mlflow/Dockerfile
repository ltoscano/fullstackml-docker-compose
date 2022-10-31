FROM python:3.10-slim-buster
RUN apt update
RUN apt install -y build-essential gcc
# Install python packages
COPY requirements.txt /tmp
RUN pip install -r /tmp/requirements.txt
