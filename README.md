# ShapeChange-docker
A simple docker container for using the ShapeChange transformation tool (v2.11) for processing application schemas for geographic information

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
To execute a transformation, move your shapechange configuration and data models to some folder, `[local folder]`
To use the container mount the folder and run the container following command to execute a ShapeChange transformation:
```bash
docker run --rm -it -v [local folder]:/io shapechange
```
This command will open the container with an interactive shell.
The following commands can be used to run a basic ShapeChange transformation with a configuration file `config.xml` saved to the `[local folder]`
```bash
java -jar /ShapeChange/ShapeChange-2.11.0.jar -Dfile.encoding=UTF-8 -c /io/config.xml
```

**Tip:** use `$(pwd)` or `${pwd}` to select the current working directory when mounting a volume in bash or powershell respectively. See [docker documentation](https://docs.docker.com/engine/reference/commandline/run/#mount-volume--v---read-only) for more information.

**Note:** For simplicity, mounted ShapeChange configuration files should reference input and output paths using absolute paths to the `/io` folder to ensure input schema can be read from the mounted folder and written output schema are also written to your host machine. For example:
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

Optionally, this docker container can accept variables at runtime for replacing variables in configuration files. For example the variables `$input$` and `$output$` can be used to specify the input model/schema filename and output directory:
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
Thus using the following command input and output files and folders can be declared:
```bash
docker run --rm -v [local folder]:/io shapechange /io/[shapechange configuration file] -x '$input$' '/io/[input file]' -x '$output$' '/io/'
```
For example with a ShapeChange configuration file and input file called `config.xml` and `input.xmi` located in your current working directory in a unix bash shell 
```bash
java -jar /ShapeChange/ShapeChange-2.11.0.jar -Dfile.encoding=UTF-8 -c /io/config.xml -x '$input$' '/io/input.xmi' -x '$output$' '/io/'
```
