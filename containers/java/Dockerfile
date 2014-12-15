FROM ubuntu:precise

# install add-apt-repository tool
RUN apt-get install -y python-software-properties

# Java 7 apt repository
RUN add-apt-repository ppa:webupd8team/java

RUN apt-get update

# auto accept oracle jdk license
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java7-installer

RUN apt-get install -y wget