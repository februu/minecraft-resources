# Minecraft Resources

Here I put all Minecraft server scripts, Dockerfiles, stash resource packs that I create and more. If you need more information about them, just scroll down! 😊

- [Febru Tweaks Resource packs](#febru-tweaks-resource-packs)
   * [Febru's Tweaks 1.21](#februs-tweaks-121)
   * [Febru's Tweaks 1.21.4](#februs-tweaks-1214)
- [Febru Server Dockerfiles](#febru-server-dockerfiles)
- [Febru MC Bash Scripts](#febru-mc-bash-scripts)
   * [run.sh](#runsh)

## Febru Tweaks Resource packs

In `resource_packs` folder you can find stash texture packs that I created from what I could gather all over the Internet. I made them to make Minecraft feel more alive but still keep its vanilla feel. If you prefer to add packs one-by-one or are just curious whats inside, look no further than below.

### Febru's Tweaks 1.21

- [Summer Day Panorama](https://modrinth.com/resourcepack/summer-day-panorama)
- [Low Shield Pack](https://modrinth.com/resourcepack/low-shield-pack)
- [Low On Fire](https://modrinth.com/resourcepack/low-on-fire)
- [Cubic Sun & Moon](https://modrinth.com/resourcepack/cubic-sun-moon)
- [Aimz PvP Crosshair](https://www.curseforge.com/minecraft/texture-packs/aimz-pvp-crosshair)
- [Better Leaves](https://modrinth.com/resourcepack/better-leaves)
- [Borderless Glass](https://modrinth.com/resourcepack/borderless-glass)
- [Fast Better Grass](https://modrinth.com/resourcepack/fast-better-grass)
- [Invisible Helmets](https://modrinth.com/resourcepack/invisible-helmets)

### Febru's Tweaks 1.21.4

All of the above from 1.21 (without Summer Day Panorama) +

- [Better Lanterns](https://modrinth.com/resourcepack/better-lanterns)
- [Cherry Background](https://modrinth.com/resourcepack/cherry-background)
- [Crops 3D](https://www.curseforge.com/minecraft/texture-packs/crops-3d)
- [Theone's Eating Animation Pack](https://modrinth.com/resourcepack/theones-eating-animation-pack)
- [Spawned Eggs](https://modrinth.com/resourcepack/spawned-eggs)

I also recommend using [Invisible Item Frames](https://modrinth.com/resourcepack/invisible-item-frames) and [Fresh Animations](https://www.curseforge.com/minecraft/texture-packs/fresh-animations). If you use sodium, you'll need to install [Entity Model Features](https://modrinth.com/mod/entity-model-features) & [Entity Texture Features](https://www.curseforge.com/minecraft/mc-mods/entity-texture-features-fabric) mods for latter to work properly.

## Febru Server Dockerfiles

In this repo you can find two dockerfiles: `Dockerfile.fabric` and `Dockerfile.purpur`. You can use them to build docker images for [Fabric Server](https://fabricmc.net/use/server/) or my beloved [Purpur](https://purpurmc.org/). The commands to build both images and run them as containers are provided below.

To build a docker image clone this repo and run this command. Change the filename to `Dockerfile.fabric` if you want to build a Fabric image. You can also set the tag to whatever you want. There are also additional arguments you can add or edit inside Dockerfile to change the Minecraft version. Default is 1.21.5 for Fabric and 1.21.4 for Purpur.

```bash
docker build -f Dockerfile.purpur -t purpur-mc .
```

Run the container using the command below. This will run a container with name `purpur-server`, max memory size of 4 GB, server files will be stored in ./purpur-server directory, port 25565 will be opened and the container will automatically restart until stopped manually by docker command (using /stop inside container or on the server will cause it to restart - pretty neat right?).

```bash
docker run -d \
  --name purpur-server \
  -e MEMORYSIZE=4G \
  -v ./purpur-server:/data \
  -p 25565:25565 \
  --restart unless-stopped \
  purpur-mc
``` 

If you want to modify config files without having to sudo all the time, just make yourself the owner of the entire ./purpur-server folder. Run this command after the container is run and all the files are created.

```bash
sudo chown -R $(id -u):$(id -g) ./febru-fabric
```

## Febru MC Bash Scripts

In the `scripts` folder you can find different scripts that will help you to manage your Minecraft server. You can find the list of all scripts with their descriptions below:

### run.sh

This simple script takes care of your Minecraft server restarts. It also creates backup of your world by zipping world, world_nether and world_the_end directories and putting them in backup folder. What's more, it deletes the backup files if they are older than 7 days. In version 1.1 I also added Aikar's flags which make your server's performance a little bit better.

Usage:

```bash
./run.sh <server_file_name.jar> <memory_amount> <days_to_keep_backups>
```

You can find more info about the setup of this script here: [https://github.com/februu/mc-bash](https://github.com/februu/mc-bash).