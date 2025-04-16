FROM eclipse-temurin:21-jre-alpine

# Defines the version of the server
ARG MC_VERSION=1.21.5
ARG LOADER_VERSION=0.16.13
ARG INSTALLER_VERSION=1.0.3

# Defines max server memory size
ARG MEMORY=4G
ENV MEMORYSIZE=$MEMORY

WORKDIR /server

# Downloads fabric loader binary
ADD https://meta.fabricmc.net/v2/versions/loader/${MC_VERSION}/${LOADER_VERSION}/${INSTALLER_VERSION}/server/jar loader.jar

WORKDIR /data

# Defines volume to store world/configs/etc.
VOLUME /data

# Aikar's flags
ENV JAVAFLAGS="-XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=mcflags.emc.gs -Dcom.mojang.eula.agree=true"

ENTRYPOINT java $JAVAFLAGS -Xms$MEMORYSIZE -Xmx$MEMORYSIZE -jar /server/loader.jar nogui
