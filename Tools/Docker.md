# Docker cheatsheet

image filesystem
 host’s filesystem

Clone a project with a `Dockerfile` file (= instructions how to assemble the private filesystem)

## Build
```
docker build --tag bulletinboard:1.0 .
```

## Run
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```
