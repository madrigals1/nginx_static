# Nginx Static Hosting

Project for hosting static files using **Nginx + Docker**.

## Prerequisites

Make sure you have installed these:
- [Docker and Docker Compose](https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04) - Will install all the required packages and software.
- (Optional) [Dockerized Nginx with SSL](https://github.com/madrigals1/nginx) - Will generate SSL certificates and make the app accessible through `SSL_DOMAIN`, that is set inside `.env`.

## Installation

Make a copy of `.env.example` file named `.env`

```shell script
cp .env.example .env
```

---

Environment variables:
- `PORT` - port on which the app will be running.
- `DOCKER_STATIC_HOSTING` - place, where we will save all of our files.
- SSL settings (Not needed without **Dockerized Nginx**):
    - `SSL_DOMAIN` - domain of the website with VizAPI
    - `LETSENCRYPT_EMAIL` - Email for LetsEncrypt notifications.
    - `HTTPS_NETWORK` - network, in which our HTTPS server will be running. 

```dotenv
PORT=8800
DOCKER_STATIC_HOSTING=/var/www/static

# Letsencrypt settings
SSL_DOMAIN="static.example.com"
LETSENCRYPT_EMAIL="user@example.com"
HTTPS_NETWORK=https_network
```

---

Create network with the name, that we have in `HTTPS_NETWORK` environment variable.

```shell script
docker network create nginx-proxy
```

---

Build the Docker image

```shell script
docker-compose build
```

## Running

Start
```
docker-compose up
```

Stop
```
docker-compose down
```

## Usage

- Put any file inside `DOCKER_STATIC_HOSTING/<path_to_the_file>` folder.
- File will be accessible under `<url>/<path_to_the_file>`
> `<url>` will be `localhost:PORT` if running without **Dockerized Nginx** and `SSL_DOMAIN` if running with **Dockerized Nginx**

## Authors
- Adi Sabyrbayev [Github](https://github.com/madrigals1), [LinkedIn](https://www.linkedin.com/in/madrigals1/)
