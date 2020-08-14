FROM maven:3.6.3-jdk-8 as builder

ARG git_name="Max Mustermann"
ARG git_email="max.mustermann@gmail.com"
ARG version=master
 
RUN apt-get update && apt-get install --assume-yes patch 
WORKDIR /tmp/

RUN git config --global user.email $git_email
RUN git config --global user.name $git_name
RUN git clone https://github.com/PaperMC/Paper.git
RUN cd Paper/ && git checkout $version && ./paper jar

FROM openjdk:14-alpine
WORKDIR /root/
RUN echo eula=true >> eula.txt
COPY --from=builder /tmp/Paper/paperclip.jar /root/paperclip.jar

COPY log4j2.xml /root/
CMD ["java", "-Dlog4j.configurationFile=log4j2.xml", "-Xms10G", "-Xmx10G", "-XX:+UseG1GC", "-XX:+ParallelRefProcEnabled", "-XX:MaxGCPauseMillis=200", "-XX:+UnlockExperimentalVMOptions", "-XX:+DisableExplicitGC", "-XX:+AlwaysPreTouch", "-XX:G1NewSizePercent=30", "-XX:G1MaxNewSizePercent=40", "-XX:G1HeapRegionSize=8M", "-XX:G1ReservePercent=20", "-XX:G1HeapWastePercent=5", "-XX:G1MixedGCCountTarget=4", "-XX:InitiatingHeapOccupancyPercent=15", "-XX:G1MixedGCLiveThresholdPercent=90", "-XX:G1RSetUpdatingPauseTimePercent=5", "-XX:SurvivorRatio=32", "-XX:+PerfDisableSharedMem", "-XX:MaxTenuringThreshold=1", "-Dusing.aikars.flags=https://mcflags.emc.gs", "-Daikars.new.flags=true", "-jar", "/root/paperclip.jar", "nogui", "-S", "/root/configs/spigot.yml", "-paper", "/root/configs/paper.yml", "-c", "/root/configs/server.properties", "-b", "/root/configs/bukkit.yml"]
