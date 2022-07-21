# Docker intro

## Terminologies

- host machine
  - docker 가 설치되어 있는 컴퓨터
  - container 안과 구분하기 위해 사용하는 용어임.
- registry
  - docker repository 들이 등록되어 있음.
  - Docker Hub
- repository
  - A repository is a set of Docker images. A repository can be shared by pushing it to a registry server. The different images in the repository can be labeled using tags.
- tag
- image
- container
- network

additionally

- docker compose
- docker swarm
- Kubernetes

## How to run an image as a container

```bash
docker run -it -n hello_container hello-world
```

- 이미지가 로컬 registry 에 없다면 자동으로 Docker Hub 에서 이미지를 다운로드 받는다.
- Docker가 container 를 만들어 실행한다.

주요 옵션

- `-i` 는 interactive하게 입력과 출력 container 의 내부로부터 주고 받는다. 보통 `-it` 로 사용한다.
- `-t`는 terminal 을 연결해서 표시해주겠다는 의미이다 보통은 `-it`로 사용한다.
- `--name hello_container` 은 container 의 이름을 `hello_container` 로 지정한다는 의미이다. 지정하지 않을 경우 Docker가 임의로 이름을 생성하여 사용한다.
- `-e ABC=DEF` 환경 변수를 container 에 세팅하여 실행한다.
- `-p 1234:5678` 호스트 머신의 포트인 1234 를 컨테이너 안의 5678에 매핑한다.
- `-v /home/abcd/data:/data` 호스트 머신의 `/home/abcd/data` 폴더를 컨테이너 안의 `/data` 폴더에 연결한다. (bind mount)
  - `https://docs.docker.com/storage/bind-mounts/`
- `-d` 떨어진(detached) 상태로 container를 실행한다.
- `--rm` container 의 프로세스가 종료하면 container를 자동으로 삭제한다.

## Managing containers

```bash
docker ps -a
docker container ls -a
```

- docker container 목록을 본다.
- `-a` 옵션은 현재 stop 된 container 목록까지 보여준다.

```bash
docker inspect container_name
```

- container의 상세 정보를 본다.

```bash
docker logs container_name
```

- container 의 로그를 본다.
- `-f` 옵션을 사용하면 실행중인 container의 실시간 로그를 계속 지켜볼수있다.

```bash
docker rm container_name
```

- 이름이 `container_name` 인 컨테이너를 지운다.
- `-f` 옵션을 사용하면 실행중인 컨테이너도 지울 수 있다.

```bash
docker start container_name
```

- 정지되어 있는 컨테이너를 시작한다.

```bash
docker stop container_name
```

- 실행중인 컨테이너를 정지시킨다.

```bash
docker restart container_name
```

- 실행중인 컨테이너를 재시작한다.

## Managing images

```bash
docker images
docker image ls
```

```bash
docker rmi image_name
```

```bash
docker pull
```

## Managing networks

```bash
docker network ls
```

```bash
docker network rm network_name
```

## Etc

```bash
docker system prune
```

사용하지 않는 container/image/network/cache 등을 삭제한다.

## Dockerfile

예)

```Dockerfile
FROM python:3-alpine
WORKDIR /usr/src/app
EXPOSE 8000
COPY requirements.txt .
RUN pip install -qr requirements.txt
COPY server.py .
CMD ["python3", "./server.py"]
```

## etc.

- 특별한 이유가 없으면 `ADD`보단 `COPY`를 쓴는 것을 추천
- `CMD`는 argument 들만 바꿀수는 없지만 커맨드 전체를 바꿀 수 있다. `ENTRYPOINT` 는 기본적으로 커멘들 바꾸지 않고 argument 들을 추가하여 실행된다. 커맨드는 유지하고 argument드은 디폴트 값을 지정하고 싶은 경우 커맨드는 `ENTRYPOINT`로 하고 argument 부분만 `CMD`를 쓰는 식으로 경우에 따라 둘 다 쓰는 것도 가능하다.

## References

- [docker example with Flask](https://github.com/datawire/hello-world)
- https://docker-curriculum.com/
