+++
title = "A brief introduction to Airflow"
menu = "Blog"
date = "2025-12-24"
weight = 1
draft = true
+++

# A Brief Introduction to Airflow

The purpose of this post is to help readers understand what Airflow is at a high level.

Apache Airflow is a data orchestration tool, which is a fancy way to say that it organizes your python scripts and run them one after the other 

What problem does Airflow exactly solve?
Imagine you have to run an ETL process where you ingest data from an object store like AWS S3, process that data using python, and load that data back into a table (say a table in Athena). Well, you can write a python script and schedule it using a cron job on a EC2 machine. Here is the problem, how do you monitor such a daily process? You can log into the EC2 machine and check if there are errors in the log file.

A workflow like above can be expressed in the form of a DAG (Directed Acyclic Graph). Airflow calls these workflows as DAGs. Acyclic because two steps cannot depend on each other i.e if there are two steps in the process A and B step A can depend on step B or step B can depend on step A, but both steps A and B cannot depend on each other.
Each execution of these DAGs is called as **run** and every step in this DAG is called as **task**. You define a task using an **operator**, for instance, if you want to run a python function you use a PythonOperator, if you want to run a bash script there is a BashOperator provided by Airflow.

## Architecture of Airflow

Airflow has a master slave architecture, you have web-server(master) where you can start or trigger a DAG, the web-server also provides a UI where you can check the status of each job

Airflow consists of following main components, each of these components can all run on the same machine or on different machines - 
1. Web-server 
2. Worker - This is the process that actually runs the process/function that you specify in the operator.
3. Scheduler - Lets assume you have 10 different DAGs all running at the same time, how do you ensure which job runs after the other. One way to solve this issue is put the tasks from DAGs in a queue and assign ta
4. Database - Airflow uses a database to store all the data regarding 

In most production setups, Airflow is running in a distributed fashion i.e you have a web-server that serves the UI and workers where the actual data gets processed. The workers and web-server communicate via REST APIs. Airflow also uses a database to store all the details about dags, jobs, runs etc.

Airflow acts like both a library and an application. 



### Providers




## Important configuration 

Airflow has hundreds of configuration to setup when you get started, but there are few that you absolutely need to change/tune when you are setting up it in production. It can be quite overwhelming looking at the airflow.cfg file as it is very long (2000 lines long, well, that includes their extensive documentation for every config)

Following are the important ones - 
1. sql_alchemy_conn - 
2. base_url - 
3. worker_concurrency - 
4. executor - 
5. celery_broker_url - 
6. max_active_runs_per_dag -  
7. dags_folder - 


Official Airflow configuration reference - https://airflow.apache.org/docs/apache-airflow/stable/configurations-ref.html

References
- 

This post is written by Human!