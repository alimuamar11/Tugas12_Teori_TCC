# Getting Start With Compose

1. Make sure you have been instaled compose https://docs.docker.com/compose/install/ 

2. create directori called "composetest"

3. In that directori create file app.py 

in that file, redis is the hostname of the redis container on the application’s network. We use the default port for Redis, 6379.

4. Create another file called requirements.txt

5. Create a Dockerfile

``FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
CMD ["flask", "run"]``

this tell docker to
``Build an image starting with the Python 3.7 image.
Set the working directory to /code.
Set environment variables used by the flask command.
Install gcc so Python packages such as MarkupSafe and SQLAlchemy can compile speedups.
Copy requirements.txt and install the Python dependencies.
Copy the current directory . in the project to the workdir . in the image.
Set the default command for the container to flask run``

6. Define services in a Compose file

This Compose file defines two services: web and redis.
#Web service

The web service uses an image that’s built from the Dockerfile in the current directory. It then binds the container and the host machine to the exposed port, 5000. This example service uses the default port for the Flask web server, 5000.
#Redis service

The redis service uses a public Redis image pulled from the Docker Hub registry.

7. Build and run your app with Compose

8. Lets go to web browser