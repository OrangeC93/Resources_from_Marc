docker compase ps
astro dev ps

# one way: dev_containers
Install dev_containers + Reopen code in an container + In docker app, you will see a new docker container with a different name for you

Install python in dev container, so python auto comapletion reminder will come up again

Interact with new provider: install that provider for this Docker container
- pip install apache-airflow-providers-airbyte
- go to python extension -> setting -> under remote & remote both -> edit setting.json (x not work)
- go to dockerfile add (work)
```
RUN pip install apache-airflow-providers-airbyte==3.4.0
USER root
RUN cp - r /home/astro/.local/lib/python3.11/site-packages/* /user/local/lib/python3.11/site-packages
USER astro
```

# another way: docker-compose.yaml
- create docker file:
```
FROM apache/airflow:2.7.2
RUN pip install apache-airflow-provider-airbyte
```
- left bottom: add dev container configuration files
- installl python, change python version at the right bottom
- here you go - auto completion!

