# Docker cheatsheet

- image filesystem
- host's filesystem

Clone a project with a `Dockerfile` file (= instructions how to assemble the private filesystem)

An **Image** is a set of files which has no state (it has multiple versions, like a git repository)

A **Container** is the instantiation of a Docker Image.

## Build
Build an image
```
docker build --tag bulletinboard:1.0 .
```

## Run
Run an image in a container
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```

## [Instructions](https://docs.docker.com/engine/reference/builder/#from)
- `RUN` = image build step [many] (ex: install library)
- `CMD` = which command to run on start, after the image is built [only 1] (ex: `CMD ["python", "./app.py"]`)

## [Docker compose](https://docs.docker.com/compose/compose-file/compose-file-v3/)
- ports: (HOST:CONTAINER)