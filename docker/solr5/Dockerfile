FROM ubuntu:16.04

MAINTAINER Kamil Ronewicz <galileox86@gmail.com>

RUN apt-get update && apt-get install -y \
        openjdk-8-jdk \
        wget

RUN wget http://apache.mirror1.spango.com/lucene/solr/5.5.0/solr-5.5.0.tgz

RUN tar -xzf solr-5.5.0.tgz && mv solr-5.5.0 solr && rm -rf solr-5.5.0.tgz

WORKDIR /solr

COPY vendor/ezsystems/ezplatform-solr-search-engine/lib/Resources/config/solr/* /solr/example/solr/collection1/conf/

CMD bin/solr start -f
