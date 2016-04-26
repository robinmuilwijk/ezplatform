FROM ubuntu:16.04

MAINTAINER Kamil Ronewicz <galileox86@gmail.com>

RUN apt-get update && apt-get install -y \
        openjdk-8-jdk \
        wget

RUN wget http://archive.apache.org/dist/lucene/solr/4.10.4/solr-4.10.4.tgz

RUN tar -xzf solr-4.10.4.tgz && mv solr-4.10.4 solr4 && rm -rf solr-4.10.4.tgz

WORKDIR /solr4

CMD bin/solr start -f
