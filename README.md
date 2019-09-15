# flaskrepo
[ec2-user@ip-172-31-2-28 web]$ cat app.py
from flask import Flask
from datetime import datetime
from flask import Flask, request
from flask_json import FlaskJSON, JsonError, json_response, as_json

app = Flask(__name__)
FlaskJSON(app)


@app.route('/get_time')
def get_time():
    now = datetime.utcnow()
    return json_response(time=now)

@app.route('/')
def hello_world():
    return 'Flask Dockerized'

if __name__ == '__main__':
    app.run(debug=True,host='0.0.0.0')
	
[ec2-user@ip-172-31-2-28 web]$ cat requirements.txt
Flask==1.1.1
Flask-JSON==0.3.4
[ec2-user@ip-172-31-2-28 web]$ cat Dockerfile
FROM ubuntu:latest
MAINTAINER Rajdeep Dua "dua_rajdeep@yahoo.com"
RUN apt-get update -y
RUN apt-get install -y python-pip python-dev build-essential
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
Build the docker Image
Run the following command to build the docker image flask-sample-one from web directory

$ docker build -t flask-sample-one:latest .
Run the Docker Container
$ docker run -d -p 5000:5000 flask-sample-one
