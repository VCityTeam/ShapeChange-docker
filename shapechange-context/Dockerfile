FROM eclipse-temurin:11-jre

### init dependencies
RUN apt -y update && apt -y upgrade
RUN apt install unzip

# setup shapechange
RUN mkdir /ShapeChange 
WORKDIR /ShapeChange
RUN wget https://shapechange.net/resources/dist/net/shapechange/ShapeChange/2.11.0/ShapeChange-2.11.0.zip \
 && unzip ShapeChange-2.11.0.zip

CMD [ "/bin/bash" ]