# Parrot Olympe Docker
Docker image that contains a modified version of Parrot Olympe withouth a virtualenv

## Getting Started

### Prerequisities


In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)

### Usage

#### Container Parameters

Python in the container

```shell
docker run -it dpulpeiro/parrot-olympe:1.8.0-python3.7-slim-buster python
```

Shell in the container 

```shell
docker run -it dpulpeiro/parrot-olympe:1.8.0-python3.7-slim-buster bash
```
#### Example of customized dockerfile and usage for your app

```dockerfile
FROM dpulpeiro/parrot-olympe:1.8.0-python3.7-slim-buster

COPY your-requirements /app/requirements.txt

RUN pip install --no-cache-dir -r /app/requirements.txt

```
Build your customized image

```shell
docker build -t your-image . 
```

Usage with a shell in the root of your application

```shell
docker run -it -v $PWD:/app your-image python your-main-file.py
```

#### Useful File Locations

* `/olympe` - Olympe installation files
* `/app` - Working directory

## Find Us

* [GitHub](https://github.com/your/repository)
* [Quay.io](https://quay.io/repository/your/docker-repository)


## Authors

* **Daniel García Pulpeiro** - ** - [dpulpeiro](https://github.com/dpulpeiro)

## License

This project is licensed under the MIT License - see the [LICENSE.md](https://github.com/dpulpeiro/parrot-olympe-docker/LICENSE.md) file for details.
