# syntax=docker/dockerfile:1
FROM continuumio/miniconda3:23.10.0-1

RUN apt-get update && apt-get install -y build-essential ghostscript git git-annex openssh-client

WORKDIR /tmp/
RUN wget https://mirrors.sarata.com/gnu/gsl/gsl-2.7.tar.gz && \
    tar -zxvf gsl-2.7.tar.gz && \
    cd gsl-2.7 && \
    ./configure && \
    make -j 8 && \
    make install && \
    cd .. && \
    rm -rf gsl-2.7.tar.gz gsl-2.7

COPY environment.yml /tmp/environment.yml
