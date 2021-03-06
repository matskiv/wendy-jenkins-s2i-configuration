FROM ubuntu:12.04.5

MAINTAINER Adam Saleh <asaleh@redhat.com>

USER root
# Install headless Java

ENV HOME=/home/jenkins

RUN apt-get update && \
    apt-get -y install software-properties-common python-software-properties && \
    add-apt-repository -y ppa:openjdk-r/ppa && \
    add-apt-repository ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get -y install gcc-4.8 make memcached ant bc curl wget gettext git openjdk-8-jdk lsof unzip zip liblog4cxx10-dev bzip2 g++-4.8 && \
    wget http://ftp.us.debian.org/debian/pool/main/n/nss-wrapper/libnss-wrapper_1.1.3-1_amd64.deb && \
    dpkg -i libnss-wrapper_1.1.3-1_amd64.deb && \
    wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 -O /usr/bin/jq && \
    chmod +x /usr/bin/jq && \
    apt-get install -f && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50 && \
    update-alternatives --install /usr/bin/cc cc /usr/bin/gcc-4.8 50 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50 && \
    mkdir -p /opt/feedhenry/fh-dynoman/dynos/  && \
    chmod -R 777 /opt/feedhenry/fh-dynoman/dynos/  && \
    mkdir -p /opt/feedhenry/fh-dynoman/state/  && \
    chmod -R 777 /opt/feedhenry/fh-dynoman/state/ && \
    mkdir -p /home/jenkins

RUN echo default:x:1001:0:root:/home/jenkins:/bin/bash >> /etc/passwd

ADD contrib/bin/* /usr/local/bin/

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

RUN curl -L https://github.com/openshift/origin/releases/download/v1.4.1/openshift-origin-client-tools-v1.4.1-3f9807a-linux-64bit.tar.gz | \
    tar -zx && \
    mv openshift*/oc /usr/local/bin && \
    rm -rf openshift-origin-client-tools-*

# Run the Jenkins JNLP client
ENTRYPOINT ["/usr/local/bin/run-jnlp-client"]