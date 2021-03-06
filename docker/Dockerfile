FROM ubuntu:14.04
MAINTAINER Leo Wang <grakiss.wanglei@huawei.com>
LABEL version="0.1" description="OPNFV Dovetail Docker Container"

ARG BRANCH=master

RUN \
    apt-get update \
&& \
    apt-get install -y \
        build-essential \
        gcc \
        git \
        libssl-dev \
        libffi-dev \
        vim \
        python-dev \
        python-mock \
        python-pip \
        apt-transport-https \
        wget \
        --no-install-recommends \
&& \
    apt-get update

RUN easy_install -U setuptools==30.0.0

RUN wget -qO- https://get.docker.com/ \
| \
    sed 's/-q docker-ce/-q docker-ce=17.03.0~ce-0~ubuntu-trusty/' \
| \
    sed 's/edge/stable/' \
| \
    sh

ENV HOME /home/opnfv
ENV REPOS_DIR ${HOME}/dovetail
WORKDIR /home/opnfv

RUN \
    mkdir -p ${REPOS_DIR} \
&& \
    git config --global http.sslVerify false \
&& \
    pip install git+https://git.opnfv.org/dovetail@$BRANCH#egg=dovetail \
&& \
    ln -s /usr/local/lib/python2.7/dist-packages/dovetail ${REPOS_DIR}/dovetail

WORKDIR ${REPOS_DIR}/dovetail

# get db schema from opnfv sites
# RUN mkdir -p ${REPOS_DIR}/dovetail/utils/local_db
# ADD get_db_schema.py ${REPOS_DIR}/dovetail/utils/local_db
# RUN cd ${REPOS_DIR}/dovetail/utils/local_db && python get_db_schema.py
