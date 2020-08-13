# PaperMC Docker Container
FYI: This container contains a mongodb instance. You can remove it fully from the `docker-compose.yml`if you don't want to use it. It's inside this project because it will be used for a other minecraft server project. Further if you want to use the mongodb you should remove the port forwarding from the `docker-compose.yml`. : 
```yml
...
  ports:
      - '27017-27019:27017-27019'
...
```
## Build
You can build the server with:
```bash
docker-compose build
```
Before build please fill your email address and your name for the git clone in the `docker-compose.yml`:
```yml
...
        args:
            git_name: "Max Mustermann"
            git_email: "max.mustermann@musterdomain.de"
            version: "master"
...
```
Master still builds the latest version, otherwise you can watch all possible versions at https://github.com/PaperMC/Paper/branches
, but not every old version works!

## Start
You can start the server with:
```bash
docker-compose up -d
```

## Stop
You can stop the server with:
```bash
docker-compose down
```

## Open Console
You can enter the console with:
```bash
docker attach minecraft
```

You can leave the console with
`CTRL + p, CTRL + q`.

You find the most files of the minecraft server in `./data/minecraft/`. The most data will be created after the first server start.
