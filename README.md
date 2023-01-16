# observatory-lab-server

![Continuous Integration](https://github.com/emukupa/observatory-lab-server/actions/workflows/main.yml/badge.svg)

## Docker integration summary

1. Why Docker integration?
2. Dockerize the application
3. Immediate file changes using volumes
4. Using vs-code in a docker container
5. Using docker compose
6. Using more services

## 1. Why Docker integration

More than just a virtual machine, Docker integration is an isolated environment for all dependencies, multiple services, easy deployment, same environment for collaborators, and program versions etc.

## 2. Dockerize the application

- Create a requirement.txt file and add dependencies

```txt
fastapi
uvicorn
```

- Create a src directory and add a main.py file and the code below

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "world"}
```

- In the root directory, create a Dockerfile and paste the code below

```Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY ./src ./src

CMD ["uvicorn", "src.main.app", "--host", "0.0.0.0", "--port", "8090", "--reload"]
```

- Build the image with the following command `docker build -t image-name .`
- Run the container with this command `docker run --name container-name -p 80:80 image-name`
