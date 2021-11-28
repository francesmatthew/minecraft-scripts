# Locations of relevant files:
* `/usr/bin/minecraft/` contains all mc-* scripts
* `/usr/lib/minecraft/` contains the server files

# Steps to spinning up a minecraft server

* `#` commands requires root privileges
* `$` commands requires user-level privileges

## 1) Dependencies
```
# apt-get update
# apt-get upgrade -y
# apt-get install -y openjdk-8-jre-headless git wget cron
```

## 2) Create Users
```
# useradd minecraft
# useradd -G sudo,minecraft user
# passwd user
# chsh -s /bin/bash user
# chsh -s /bin/bash minecraft
```

## 3) systemd Config
```
# mv minecraft.service /etc/systemd/system/minecraft.service
# mv minecraft.conf /usr/lib/tmpfiles.d/minecraft.conf
# systemctl daemon-reload
# systemctl enable minecraft.service
```

## 4) Minecraft Scripts
```
# mkdir /usr/bin/minecraft
# mv mc-* /usr/bin/minecraft/
# chown -R minecraft:minecraft /usr/bin/minecraft
# chmod 764 /usr/bin/minecraft/mc-*
```

## 5) Minecraft Libs/Server Jar
_Note: currently, the user must install the server _`.jar`_ file themselves_
```
# mkdir /usr/lib/minecraft
# echo eula=true > /usr/lib/minecraft/eula.txt
# chown -R minecraft:minecraft /usr/lib/minecraft
```

## 6) Optional Features
* place minecraft script directory in PATH
```
# sudo nano /etc/environment
```
* world backup cron job
_Note: this feature is not working in the current version_
```
# systemctl enable cron
```
