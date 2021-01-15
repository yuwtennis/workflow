
SHELL := /bin/bash
VIRTUALENV ?= ~/Devel/py3
AIRFLOW_VERSION := 1.10.14
DB_CONTAINER := docker_db_1

DB_HOST := localhost:5432
DB_USER := postgres
DB_PASSWD := postgres
DB_NAME := postgres

install:
	mkdir $(AIRFLOW_HOME) ; \
	cp airflow.cfg.postgresql $(AIRFLOW_HOME)/airflow.cfg
	pipenv install ; pipenv run airflow initdb
setup:
	docker cp ./airflow.sql $(DB_CONTAINER):/tmp/airflow.sql
	docker exec $(DB_CONTAINER) \
		psql 'postgresql://$(DB_USER):$(DB_PASSWD)@$(DB_HOST)/$(DB_NAME)' -f /tmp/airflow.sql
clean:
	pipenv uninstall --all ; rm -rf Pipfile.lock ; rm -rf $(AIRFLOW_HOME)
