# Docker

## What is Docker

## First Example (Python + Docker)
Create an empty folder containing two files: `myscript.py` and `Dockerfile`.

`myscript.py`
```python
import pandas
print(pandas.DataFrame())
```

`Dockerfile`
```
FROM python:3

ADD myscript.py /

RUN pip install pandas

CMD [ "python", "./my_script.py" ]

```

Build the app: `docker build -t python-dummy-app .`

See images: `docker images`

See containers: `docker ps`

Run the app: `docker run python-dummy-app`