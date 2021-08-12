FROM python:3.8.5-slim

ARG AIRFLOW_VERSION=1.10.14
ENV AIRFLOW_VERSION=${AIRFLOW_VERSION}
ENV AIRFLOW_HOME=/usr/local/airflow
ENV AIRFLOW_GPL_UNIDECODE=yes
ENV PYTHONPATH ${AIRFLOW_HOME}

LABEL application="airflow"
LABEL version="${AIRFLOW_VERSION}"

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive
ENV TERM linux

RUN apt update \
    && apt install -yqq --no-install-recommends \
       python3-dev libkrb5-dev libsasl2-dev libssl-dev \
       libffi-dev build-essential libblas-dev liblapack-dev \
       libpq-dev git \
    && apt install -yqq --no-install-recommends \
       sudo python3-pip python3-requests default-mysql-client \
       default-libmysqlclient-dev apt-utils curl rsync netcat locales

RUN sed -i 's/^# en_US.UTF-8 UTF-8$/en_US.UTF-8 UTF-8/g' /etc/locale.gen \
    && locale-gen \
    && update-locale \
    && LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 \
    && useradd -ms /bin/bash -d ${AIRFLOW_HOME} airflow

USER airflow

ENV AIRFLOW_VERSION=${AIRFLOW_VERSION}
ENV PATH=${PATH}:${AIRFLOW_HOME}/.local/bin

RUN pip install --user -U pip setuptools wheel \
   #&& pip install --user apache-airflow==${AIRFLOW_VERSION} \
   && pip install --user apache-airflow[async,aws,celery,crypto,jdbc,postgres,password]==${AIRFLOW_VERSION} \
      --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-3.8.txt" \
   && pip install --user \
    #  celery==4.4.7 \
      psycopg2-binary==2.9.1 \
      redis==3.5.3 \
    #  snowflake-connector-python==2.3.2 \
      toolz==0.10.0 \
      cattrs==1.0.0

USER root

RUN apt-get clean \
    && rm -rf \
      /var/lib/apt/lists/* \
      /tmp/* \
      /var/tmp/* \
      /usr/share/man \
      /usr/share/doc \
      /usr/share/doc-base

COPY config/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

COPY config/airflow.cfg ${AIRFLOW_HOME}/airflow.cfg
RUN chown -R airflow: ${AIRFLOW_HOME}
