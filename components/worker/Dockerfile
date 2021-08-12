FROM airflow-dependencies:1.10.14

USER root
WORKDIR ${AIRFLOW_HOME}

COPY dags ${AIRFLOW_HOME}/dags
COPY plugins ${AIRFLOW_HOME}/plugins

RUN chown -R airflow: ${AIRFLOW_HOME}

USER airflow

EXPOSE 8793
ENTRYPOINT ["/entrypoint.sh"]
