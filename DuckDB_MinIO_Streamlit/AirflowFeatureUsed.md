Pool: 
Some systems can get overwhelmed when too many processes hit them at the same time. Airflow pools can be used to limit the execution parallelism on arbitrary sets of tasks. The list of pools is managed in the UI (Menu -> Admin -> Pools) by giving the pools a name and assigning it a number of worker slots. There you can also decide whether the pool should include deferred tasks in its calculation of occupied slots.

Astro Python SDK: The create_reporting_table DAG uses the transform operator of the Astro Python SDK to make creating a reporting table from a SQL Select query simple.

Dynamic task mapping: Several tasks in this repository are dynamically mapped to adjust the number of needed mapped task instances depending on inputs at runtime.
```python
## dynamically map over the custom LocalFilesystemToMinIOOperator to read the contents of 2 local csv files to MinIO
ingest_climate_data = LocalFilesystemToMinIOOperator.partial(
  
)
```

Trigger DAG runs as soon as the climate and weather data is ready in MinIO
```python
## in include/load/loads_data.py
schedule = [gv.DS_CLIMATE_DATA_MINIO, gv.DS_WEATHER_DATA_MINIO]
```
``` python
## in include/ingestion/in_climate_data.py
outlets=[gv.DS_CLIMATE_DATA_MINIO]
## in include/ingestion/in_local_weather.py
outlets=[gv.DS_WEATHER_DATA_MINIO]
```

Airflow XCom and Airflow Variables: Small amounts of data like the current weather in the user-defined city are passed from one task to another using XCom. The coordinates of the city are saved as an Airflow Variable.

Custom operators and hooks: When interacting with MinIO the blueprint repository uses custom MinIO operators, which are stored locally in include/custom_operators/minio.py the operators use a custom Airflow hook to interact with MinIO using credentials saved in an Airflow connection.

Custom re-useable task group: The pattern of checking if a MinIO bucket of a specific name already exists and, if not, creating the bucket occurs several times in this repository. A great use case too, instead of redefining the tasks every time, use a reusable task group. Explore the task group code at include/custom_task_groups/create_bucket.py .
