<img src="https://avatars.githubusercontent.com/u/5429470?s=280&v=4" align="center" >

### Flask and Nginx Dockerized App

This project is a simple Flask application served with Nginx using Docker. The application displays a "Hello, World!" message when accessed.



### Prerequisites

- Docker
- Docker Compose


### Getting Started

##### 1. clone the repository

````
git clone https://github.com/amirhoseinshojaei/Dockerize_flask.git
````


##### 2.Build and Run the Docker Containers

``docker-compose up --build``


##### 3.Stopping Application

``docker-compose down``


#### File Descriptions

- apps.py:
```from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<h1>Hello, World by docker !</h1>"
```

- dockerfile:

```
# Use an official Python runtime as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir flask

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Define environment variable
ENV FLASK_APP=app.py

# Run app.py when the container launches
CMD ["flask", "run", "--host=0.0.0.0"]

```

- docker-compose.yaml

````
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"

  nginx:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - web

````

- default.conf


`````
upstream app {

    server app:5000;
}

server{

    listen 80;
    location / {

        proxy_pass http://app;
    }
}

`````


- nginx **dockerfile**


````
FROM nginx:alpine

RUN rm /etc/nginx/conf.d/default.conf

ADD ./default.conf /etc/nginx/conf.d
````



# License

This project is licensed under the MIT <a href="https://github.com/amirhoseinshojaei/Dockerize_flask#">Click Here</a> - see the LICENSE.md file for details.


## Happy Mood

**Be happy and Enjoy this project , And Always learning😎**

**You make me very happy by forking and committing to the project🤩**