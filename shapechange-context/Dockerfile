FROM eclipse-temurin:11-jre

### install dependencies
RUN apt update && apt install -y unzip

# install shapechange
RUN mkdir /ShapeChange 
WORKDIR /ShapeChange
RUN wget https://shapechange.net/resources/dist/net/shapechange/ShapeChange/2.11.0/ShapeChange-2.11.0.zip \
 && unzip ShapeChange-2.11.0.zip

ENTRYPOINT [ "java", "-jar", "ShapeChange-2.11.0.jar" ]
CMD [ "-Dfile.encoding=UTF-8", "-c" ]