# XMage Beta Server based on OpenJDK Alpine

This build is based on the version created by [LunarNightShade](https://github.com/LunarNightShade/docker-xmage-openjdk). I modified it to pull the most recent build of the BETA server.

## Usage
```
docker run -d -it \
    --name XMage \
    -p 17171:17171 \
    -p 17179:17179 \
    --add-host example.com:0.0.0.0 \
    -e "XMAGE_DOCKER_SERVER_ADDRESS=example.com" \
    --restart unless-stopped \
    revice02/docker-xmage-beta-server
```

XMage needs to know the domain name the server is running on. The `--add-host` option adds an entry to the containers `/etc/hosts` file for this domain. Replace `example.com` with your server IP address or domain name address.
Using the `XMAGE_*` environment variables you can modify the `config.xml` file.
You should always set XMAGE_DOCKER_SERVER_ADDRESS to the same value as your `--add-host` flag value.

---

## Available Environment Variables and Default Values

+ JAVA_MIN_MEMORY=256M
+ JAVA_MAX_MEMORY=3G
+ XMAGE_DOCKER_SERVER_ADDRESS="0.0.0.0"
+ XMAGE_DOCKER_PORT="17171"
+ XMAGE_DOCKER_SEONDARY_BIND_PORT="17179"
+ XMAGE_DOCKER_MAX_SECONDS_IDLE="600"
+ XMAGE_DOCKER_AUTHENTICATION_ACTIVATED="false"
+ XMAGE_DOCKER_SERVER_NAME="mage-server"
+ XMAGE_DOCKER_ADMIN_PASSWORD="liliana666"
+ XMAGE_DOCKER_MAX_GAME_THREADS="10"
+ XMAGE_DOCKER_MIN_USERNAME_LENGTH="3"
+ XMAGE_DOCKER_MAX_USERNAME_LENGTH="14"
+ XMAGE_DOCKER_MIN_PASSWORD_LENGTH="8"
+ XMAGE_DOCKER_MAX_PASSWORD_LENGTH="100"
+ XMAGE_DOCKER_MAILGUN_API_KEY="X"
+ XMAGE_DOCKER_MAILGUN_DOMAIN="X"

---

If you would like to preserve the database during updates and restarts you can mount a volume at `/xmage/mage-server/db` (Important if you're using user authentication). 

Add `--mount source=xmage-db,target=/xmage/mage-server/db` to your `docker run` command.

---

## Simple DNS setup for XMage

+ Go to  https://nip.io/
+ Set the domain name to `magic-xxx.xxx.xxx.xxx.nip.io` as serverAddress (`xxx.xxx.xxx.xxx` is your public IP);
+ On Server side: edit host (`/etc/hosts`) file to map that domain name `magic-xxx.xxx.xxx.xxx.nip.io` to your local IP;
+ On Client side: use normal domain name `magic-xxx.xxx.xxx.xxx.nip.io`

---

## Unraid template and configuration

You can find a template to use with unRaid's docker service here: https://github.com/revice02/unraid-templates

Make sure you edit the `Extra Parameters:	--add-host example.com:0.0.0.0` section in order to modify the containers host file.

---
