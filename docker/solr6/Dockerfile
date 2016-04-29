FROM ubuntu:16.04

MAINTAINER Kamil Ronewicz <galileox86@gmail.com>

RUN apt-get update && apt-get install -y \
        openjdk-8-jdk \
        wget

RUN wget http://ftp.ps.pl/pub/apache/lucene/solr/6.0.0/solr-6.0.0.tgz

RUN tar -xzf solr-6.0.0.tgz && mv solr-6.0.0 solr && rm -rf solr-6.0.0.tgz

WORKDIR /solr

COPY vendor/ezsystems/ezplatform-solr-search-engine/lib/Resources/config/solr/* /solr/example/solr/collection1/conf/

CMD bin/solr start -f
