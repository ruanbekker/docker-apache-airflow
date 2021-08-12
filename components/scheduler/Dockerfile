FROM airflow-dependencies:1.10.14

COPY dags ${AIRFLOW_HOME}/dags
COPY plugins ${AIRFLOW_HOME}/plugins

RUN chown -R airflow: ${AIRFLOW_HOME}

USER airflow

WORKDIR ${AIRFLOW_HOME}
ENTRYPOINT ["/entrypoint.sh"]
