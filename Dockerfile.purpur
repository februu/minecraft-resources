FROM eclipse-temurin:21-jre-alpine

# Defines the version of the server
ARG MC_VERSION=1.21.4
ARG PURPUR_TAG=2416

# Defines max server memory size
ARG MEMORY=4G
ENV MEMORYSIZE=$MEMORY

WORKDIR /server

# Downloads fabric loader binary
ADD https://api.purpurmc.org/v2/purpur/${MC_VERSION}/${PURPUR_TAG}/download purpur.jar

WORKDIR /data

# Defines volume to store world/configs/etc.
VOLUME /data

# Aikar's flags
ENV JAVAFLAGS="-XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=mcflags.emc.gs -Dcom.mojang.eula.agree=true"

ENTRYPOINT java $JAVAFLAGS -Xms$MEMORYSIZE -Xmx$MEMORYSIZE -jar /server/purpur.jar nogui
