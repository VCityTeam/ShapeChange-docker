FROM eclipse-temurin:11-jre

ARG SHAPECHANGE_VERSION=2.11.0
ENV SHAPECHANGE_VERSION=${SHAPECHANGE_VERSION}

### install dependencies
RUN apt update && apt install -y unzip

### install shapechange
RUN mkdir /ShapeChange 
WORKDIR /ShapeChange
RUN wget https://shapechange.net/resources/dist/net/shapechange/ShapeChange/${SHAPECHANGE_VERSION}/ShapeChange-${SHAPECHANGE_VERSION}.zip \
  && unzip ShapeChange-${SHAPECHANGE_VERSION}.zip

### Apparently this doesnt easily work since shapechange requires an X11 environment 
# ENTRYPOINT java -jar ShapeChange-${SHAPECHANGE_VERSION}.jar
# CMD [ "-h" ]

ENTRYPOINT [ "/bin/bash" ]