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
ADD entrypoint.sh /root/entrypoint.sh

ENTRYPOINT ["/root/entrypoint.sh"]
