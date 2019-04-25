FROM alpine:3.9

USER root

RUN mkdir -p /deployments

# JAVA_APP_DIR is used by run-java.sh for finding the binaries
ENV JAVA_APP_DIR=/deployments \
    JAVA_MAJOR_VERSION=8


# /dev/urandom is used as random source, which is perfectly safe
# according to http://www.2uo.de/myths-about-urandom/
RUN apk add --update \
    curl \
    openjdk8-jre-base=8.201.08-r1 \
 && rm /var/cache/apk/* \
 && echo "securerandom.source=file:/dev/urandom" >> /usr/lib/jvm/default-jvm/jre/lib/security/java.security
COPY hello-dropwizard-1.0.jar /opt/hello-dropwizard-1.0.jar
COPY example.yaml /opt/example.yaml

EXPOSE 8080
WORKDIR /opt
CMD java -jar hello-dropwizard-1.0.jar server example.yaml
