FROM quay.io/jupyter/minimal-notebook:python-3.12.11

USER root

RUN sudo apt-get update -y
RUN sudo apt-get install software-properties-common -y
RUN sudo apt upgrade -y

# To Install Open JDK
RUN sudo add-apt-repository ppa:openjdk-r/ppa
RUN sudo apt-get update -y
RUN sudo apt-get install openjdk-17-jdk -y

COPY ./jupyter/requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt
