FROM crunchydata/crunchy-postgres:centos7-10.5-2.1.0

USER root

RUN yum -y update; yum clean all
RUN yum -y install postgresql10-plpython supervisor; yum clean all


### Get postgres specific add-ons
RUN yum update -y && yum install -y \
                    git \
                    gcc \
                    wget \
                    postgresql10-devel \
                    openssl \
                    m4 \
                    vim \
                    flex \
                    bison \
                    graphviz \
                    java \
                    epel-release \
                    python-devel

RUN yum install -y python-pip
ENV PATH="$PATH:/usr/pgsql-10/bin"
RUN pip install awscli pygresql paramiko --upgrade

RUN mkdir -p /src/madlib
COPY ./data/apache-madlib-1.15.1-bin-Linux.rpm /src/madlib

RUN yum install -y /src/madlib/apache-madlib-1.15.1-bin-Linux.rpm --nogpgcheck

USER 26
EXPOSE 5432
CMD ["/opt/cpm/bin/start.sh"]