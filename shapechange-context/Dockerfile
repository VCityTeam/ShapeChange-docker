FROM eclipse-temurin:11-jre

ARG version=2.11.0
ENV version=${version}

### install dependencies
RUN apt update && apt install -y unzip

### install shapechange
RUN mkdir /ShapeChange 
WORKDIR /ShapeChange
RUN wget https://shapechange.net/resources/dist/net/shapechange/ShapeChange/${version}/ShapeChange-${version}.zip \
  && unzip ShapeChange-${version}.zip

### Apparently this doesnt easily work since shapechange requires an X11 environment 
# ENTRYPOINT [ "java", "-jar", "ShapeChange-${version}.jar" ]
# CMD [ "-Dfile.encoding=UTF-8", "-c" ]

ENTRYPOINT [ "/bin/bash" ]