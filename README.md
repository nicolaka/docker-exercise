## Running with Docker

Build the first version of the Flask application:

```bash
docker build -t ytrewq019283/dockerexercise:v1 .
```

For Exercise 1, start MongoDB on the host and run the application:

```bash
docker run -d --name mongo-test -p 27017:27017 mongo:3.6

docker run -d --name web-test -p 5001:5000 \
  -e MONGO_HOST=host.docker.internal \
  ytrewq019283/dockerexercise:v1
```

For Exercise 2, build and push the second image:

```bash
docker build -t ytrewq019283/dockerexercise:v2 .
docker push ytrewq019283/dockerexercise:v2
```

Start both services:

```bash
docker compose up
```

Open http://localhost:5001 in your browser.

Stop the services:

```bash
docker compose down
```