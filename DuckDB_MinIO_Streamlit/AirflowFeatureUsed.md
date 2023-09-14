Pool: 
Some systems can get overwhelmed when too many processes hit them at the same time. Airflow pools can be used to limit the execution parallelism on arbitrary sets of tasks. The list of pools is managed in the UI (Menu -> Admin -> Pools) by giving the pools a name and assigning it a number of worker slots. There you can also decide whether the pool should include deferred tasks in its calculation of occupied slots.


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
