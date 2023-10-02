https://www.youtube.com/watch?v=xUKIL7zsjos

```
astro dev init
```

dag/find_activity.py
```python
from airflow.decorators import dag, task
from airflow.models import Variable
from pendulumn import datetime
import request
API = 'https://www.boredapi.com/api/activity'

@dag(
    start_date=datetime(2023,1,1),
    schedule='@daily',
    tags=['activity'],
    catchup=False,
)

def find_activity():
    @task
    def get_activity():
        r = requests.get(API, timeout=10)
        return r.json
    @task
    def write_activity_to_file(response): # add variable with key: activity_file, value: /temp/activity.txt in UI, output path
        filepath = Variable.get("activity_file")
        with open(filepath, "a") as f:
          f.write(f"Today: {response['activity']}\r\n")
        return filepath
    @task
    def read_actitiy_from_file(filepath):
        with open(filepath, "r") as f:
            print(f.read())

response = get_actititity()
filepath = write_activity_to_file(response)
read_activity_from_file(filepath)
```
