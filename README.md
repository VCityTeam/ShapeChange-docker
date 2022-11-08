# ShapeChange-docker
A simple docker container for using the ShapeChange transformation tool for processing application schemas for geographic information

These instructions require a basic understanding of:
- [Docker](https://docs.docker.com/get-started/overview/)
- [ShapeChange](https://shapechange.net/)

Docker can be installed from [here](https://docs.docker.com/get-docker/)
## To build image
Clone and build the image from a command line interface
```bash
git clone https://github.com/VCityTeam/ShapeChange-docker.git
docker build -t shapechange ./ShapeChange-docker/shapechange-context/
```
## How to use
Move your shapechange configuration and data models/application schemas to some folder `[local folder]`
To use the container mount the folder and run the container following command:
```bash
docker run --rm --it -v [local folder]:/io shapechange
```
This command will open the container with an interactive shell.
The following commands can be used to run a basic ShapeChange transformation
```bash
java -jar ShapeChange-2.11.0.jar -Dfile.encoding=UTF-8 -c /io/myshapechangeconfig.xml
```

**Note:** For simplicity, mounted ShapeChange configuration files should reference input and output paths using absolute paths to the `/io` folder to ensure input schema can be read from the mounted folder and written output schema are also written to your host machine (or whatever folder you wish to mount your local folder to). For example:
```xml
<input>
   <parameter name="inputFile" value="/io/[input file]"/>
   ...
</input>
...
<targets>
  <target>
    <targetParameter name="outputDirectory" value="/io/"/>
    ...
  </target>
</targets>
```

Optionally, ShapeChange can accept variables at runtime to complete configuration files. For example the variables `$input$` and `$output$` can be used to specify the input model/schema filename and output directory:
```xml
<input>
  <parameter name="inputFile" value="$input$"/>
   ...
</input>
...
<targets>
  <target>
    <targetParameter name="outputDirectory" value="$output$"/>
    ...
  </target>
</targets>
```
Thus using the following command input and output files can be declared:
```bash
java -jar lib/ShapeChange-2.11.0.jar -Dfile.encoding=UTF-8 -c /io/myshapechangeconfig.xml -x '$input$' '/io/myinputmodel.xmi' -x '$output$' '/io/'
```


**Tip:** use `$(pwd)` to select the current working directory when mounting a volume. See [docker documentation](https://docs.docker.com/engine/reference/commandline/run/#mount-volume--v---read-only) for more information.
