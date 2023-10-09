The ExternalPythonOperator: No more dependency conflicts in Apache Airflow
https://www.youtube.com/watch?v=mWQa5mWpMZ4

instance with scikit-learn==1.0, task needs scikit-learn==1.3

Options:
- run KubernetesPodOperator
- run docker operator: run on its own docker with dependencies that won't impact your instance
- run PythonVirtualenv Operator
- Run ExternalPythonOperator

![image](pics/scikit_pythonvirtualenv.png)
