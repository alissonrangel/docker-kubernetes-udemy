# Docker & Kubernetes: The Practical Guide [2022 Edition]
## Learn Docker, Docker Compose, Multi-Container Projects, Deployment and all about Kubernetes from the ground up!

# docker cli commands

## 29 Understanding Attached & Detached Containers

### docker attach {cont_id} -> container presisa estar em execução
```
Usage:  docker attach [OPTIONS] CONTAINER

Attach local standard input, output, and error streams to a running container

Options:
      --detach-keys string   Override the key sequence for detaching a container
      --no-stdin             Do not attach STDIN
      --sig-proxy            Proxy all received signals to the process (default true)
```

### docker start -a CONTAINER -> inicia o container attachado


### docker logs [OPTIONS] CONTAINER
```
Usage:  docker logs [OPTIONS] CONTAINER

Fetch the logs of a container

Options:
      --details        Show extra details provided to logs
  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes)
  -n, --tail string    Number of lines to show from the end of the logs (default "all")
  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes)
```

## 31. Entering Interactive Mode
- docker run -it CONTAINER -> opção -a (attach) é default, -i iterativo, -t terminal
- docker stop CONTAINER
- docker start -a -i CONTAINER

## 32. Deleting Images & Containers
- docker image prune -> remove todas as imagens
- docker rm CONTAINER -> remove um container que esteja parado
- docker rmi IMAGE -> remove uma imagem sem containers

## 33. Removing Stopped Containers Automatically
- docker run -it --rm IMAGE -> --rm remove o container quando ele parar 

## 34. A Look Behind the Scenes: Inspecting Images
- docker image inspect IMAGE

## 35. Copying Files Into & From A Container
- container em execução
- docker cp ../dummy/teste.txt 095216caec01:/app/teste3.txt -> envia do host para o container, mas para uma pasta que exista no container
- docker cp 095216caec01:/app/teste3.txt ../dummy -> envia do container para o host

## 36. Naming & Tagging Containers and Images
- docker build -t name:tag .
- docker run -p 8080:80 --name cont_name IMAGE

## 37. Sharing Images - Overview
- Com Dockerfile ou a própria imagem com docker push/pull

## 38. Pushing Images to DockerHub
- cria a conta gratuita no docker hub
- docker build -t {user_name}/{image_name} .
- docker login
- cria o repositório no docker hub (Oficial docker image registry)
- docker push {user_name}/{image_name}
- docker pull {user_name}/{image_name}

## 39. Pulling & Using Shared Images
- 

## 49. Named Volumes To The Rescue!
- docker run -p 80:80 -d --rm --name feedback-app -v feedback:/app/feedback feedback-node:v3
- docker volume ls 
- docker volume rm VOLUME

Removing Anonymous Volumes
We saw, that anonymous volumes are removed automatically, when a container is removed.

This happens when you start / run a container with the --rm option.

If you start a container without that option, the anonymous volume would NOT be removed, even if you remove the container (with docker rm ...).

Still, if you then re-create and re-run the container (i.e. you run docker run ... again), a new anonymous volume will be created. So even though the anonymous volume wasn't removed automatically, it'll also not be helpful because a different anonymous volume is attached the next time the container starts (i.e. you removed the old container and run a new one).

Now you just start piling up a bunch of unused anonymous volumes - you can clear them via docker volume rm VOL_NAME or docker volume prune.

## 51. Getting Started With Bind Mounts (Code Sharing)

- docker logs CONTAINER
- docker run -p 80:80 -d --rm --name feedback-app -v feedback:/app/feedback -v $(pwd):/app feedback-node:v3

Bind Mounts - Shortcuts
Just a quick note: If you don't always want to copy and use the full path, you can use these shortcuts:

macOS / Linux: -v $(pwd):/app

Windows: -v "%cd%":/app

## 53. Combining & Merging Different Volumes

- docker run -p 80:80 -d --name feedback-app -v feedback:/app/feedback -v $(pwd):/app -v /app/node_modules feedback-node:v5