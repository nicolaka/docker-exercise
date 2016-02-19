## Docker Exercise 01

**Goal:** You have a simple Python 2.7 (Flask) and Mongo app that allows users to enter messages and displays the last message entered.
There are a couple of files in this directory that are REQUIRED by the app to work:


 1. App.py is the flask app 
 2. Requirements.txt includes a list of Python packages required to run this app
 3. Templates directory for html templates used by app.py and
 4. Static directory for css files.

This app expects a MongoDB instance to be running in the background and listening to TCP PORT 27017. You can simply issue the following command
to start a mongo db instance `docker run -d -p 27017:27017 mongo:latest`. The app is started with "python app.py" from the provided directory.

**Exercises:**

1) Dockerizing: Assuming a MongoDB instance is listening on `localhost:27017`, create a Dockerfile to dockerise this app with the following requirements:

- Make sure you install python-pip and install required Python packages listed in requirements.txt(e.g pip install -r requirements.txt)
- Make sure that container created from the Dockerfile image listens to TCP PORT 5000.
- You may choose your preferred base image as long as the app works. Recommended one is 'python:2.7' image which comes with python-pip so you don't have to install it.
- Make sure to build and push this image Docker Hub. e.g 'docker push <your_docker_hub_username>/dockerexercise:v1'.
- Make sure to provide the Dockerfile in the Docker Hub repo long description section as well as inn the response to this exercise.
    
**Deliverables**: Dockerfile

**Success Criteria :** When performing 'docker run -p 5000:5000 your_hub_username/dockerexercise:v1 ' on a host running MongoDB on port 27017, the app needs to be accessible on TCP PORT 5000. Dockerfile must be present in the repo's long description.

**2) Deploying with Compose:** Assuming `docker-compose` is installed on localhost, create a docker-compose.yml file to describe the web and db services to run the same app as in Exercise 1 with the following requirements:


**Note:** As a pre-requisite for this exercise, you need to make the following changes to your app.py file:

		(-) client = MongoClient('localhost', 27017)
		(+) client = MongoClient('db', 27017)
		

		
Then, you need to build and push a new version of your image with a v2 tag: 


		docker push `<your_docker_hub_username>/dockerexercise:v2`

- the service names are web and db.
- web service needs to use the image that you created `<your_docker_hub_username>/dockerexercise:v2`.
- web service needs to bind host port 5000 to container port `5000`.
- web service needs to have db's ip address dynamically discovered using the alias "db".
- db service must use `latest` image of the official mongo image.
- db service must expose port 27017.
- db service must be passed a command argument of "--smallfiles".
   
	
**Success Criteria:** when performing a 'docker-compose up' with the produced docker-compose.yml file, the app should be working and accessible on TCP PORT 5000. `docker-compose.yml` needs to be included in the response to this exercise.


**Deliverables**: docker-compose.yml file
