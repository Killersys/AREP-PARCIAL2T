# Parcial Segundo Tercio AREP

## Requerimientos

Diseñe, construya y despliegue los siguientes servicios en un microcontenedor docker desplegado en una instancei a EC2 de AWS y otro desplegador en AWS lambda con AWS gateway. . Cada estudiante debe seleccionar para desarrollar dos funciones matemáticas de acuerdo a los dos últimos dígitos de su cédula como se especifica en la lista. Todas las funciones reciben un solo parámetro de tipo "Double" y retornan una prámetro sde tipo "Double".

0. log
1. ln
2. sin
3. cos
4. tan
5. acos
6. asin
7. atan
8. sqrt
9. exp (el número de eauler elevado ala potendia del parámetro)

Implemente los servicios para responder al método de solicitud HTTP GET. Deben usar el nombre de la función especificado en la lista y el parámetro debe ser pasado en la variable de query con nombre "value".

Ejemplo de un llamado:

https://amazonxxx.x.xxx.x.xxx:{port}/cos?value=3.141592


Lambda + API Gateway
https://amazonxxx.x.xxx.x.xxx/sin?value=3.141592



Salida. El formato de la salida y la respuesta debe ser un JSON con el siguiente formato

{
 "operation": "cos",
 "input":  3.141592,
 "output":  -0.999999
}

## Prerrequisitos
Para la realización y ejecución tanto del programa como de las pruebas de este, se requieren ser instalados los siguientes programas:
* [Maven](https://maven.apache.org/). Herramienta que se encarga de estandarizar la estructura física de los proyectos de software, maneja dependencias (librerías) automáticamente desde repositorios y administra el flujo de vida de construcción de un software.
* [GIT](https://git-scm.com/). Sistema de control de versiones que almacena cambios sobre un archivo o un conjunto de archivos, permite recuperar versiones previas de esos archivos y permite otras cosas como el manejo de ramas (branches).
* [Docker](https://www.docker.com/). Programa encargado de crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.
Para asegurar que el usuario cumple con todos los prerrequisitos para poder ejecutar el programa, es necesario disponer de un Shell o Símbolo del Sistema para ejecutar los siguientes comandos para comprobar que todos los programas están instalados correctamente, para así compilar y ejecutar tanto las pruebas como el programa correctamente.

Para asegurar que el usuario cumple con todos los prerrequisitos para poder ejecutar el programa, es necesario disponer de un Shell o Símbolo del Sistema para ejecutar los siguientes comandos para comprobar que todos los programas están instalados correctamente, para así compilar y ejecutar tanto las pruebas como el programa correctamente.

```
mvn -version
git --version
java -version
docker version
```

## Instalación
Para descargar el proyecto de GitHub, primero debemos clonar este repositorio, ejecutando la siguiente línea de comando en GIT.

```
git clone https://github.com/Killersys/AREP-PARCIAL2T.git
```

## Ejecución
Para compilar el proyecto utilizando la herramienta Maven, nos dirigimos al directorio donde se encuentra alojado el proyecto, y dentro de este ejecutamos en un Shell o Símbolo del Sistema el siguiente comando:

```
mvn package
```
## Pruebas
Para realizar las pruebas correspondientes del proyecto utilizando la herramienta Maven, nos dirigimos al directorio donde se encuentra alojado el proyecto, y dentro de este ejecutamos en un Shell o Símbolo del Sistema el siguiente comando:

```
mvn test
```

A continuación se muestran las pruebas compiladas correctamente para el código fuente.

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Prueba.PNG)

----------

### Docker

Abrimos la aplicación de Docker y verificamos que esté corriendo por el puerto usado (en este caso fue el 8000) 
![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Dockerdesktop.PNG)

Comprobamos que la aplicación funcione de manera local utilizando docker, para ello calculamos el coseno del ejemplo dado (3.141592). Para ello ingresamos en el navegador la URL: http://localhost:8000/cos?value=3.141592

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Dockercos.PNG)

Realizamos el mismo procedimiento para revisar que la función logaritmo esté funcionando. Ingresamos en la URL: http://localhost:8000/log?value=3.141592.

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Dockerlog.PNG)


----------

### AWS


Desplegamos el Docker en nuestra máquina AWS  y verificamos que esté corriendo por el puerto usado (en este caso fue el 8000) y abrimos la URL: http://ec2-100-25-220-199.compute-1.amazonaws.com:8000/log?value=3.141592. Podemos observar que se encuentra desplegada
![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Awslog.PNG)

Realizamos el mismo procedimiento para revisar que la función coseno esté funcionando. Ingresamos en la URL: http://ec2-100-25-220-199.compute-1.amazonaws.com:8000/cos?value=3.141592.

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Awscos.PNG)


----------

### Lambda

```
Paso a Paso
```

Seleccionamos el servicio Lambda

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambda.PNG)

Seleccionamos Crear Función

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambda2.PNG)

Seleccionamos Función desde cero, asignamos un nombre a la función y seleccionamos el lenguaje como "Java 8".

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambda3.PNG)

Tomamos un rol existente y creamos la función

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambda4.PNG)

Para el código fuente elegimos "cargar desde" y seleccionamos nuestro .jar 

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/lambdacarga.PNG)

Configuramos el tiempo de ejecución y añadimos el controlador

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambdaedicion.PNG)

Luego de guardar los cambios, seleccionamos la pestaña "Probar". Seleccionamos el nombre de la prueba e ingresamos un valor. Enseguida invocamos.

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambdaprueba.PNG) 

Observamos el resultado de ejecución de la prueba.

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambdaprueba.PNG)

![img](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/img/Lambdaprueba2.PNG)

----------


### Video prueba

![awsWorkingVideo](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/Sustentación.gif)  

## Construido con
* [Maven](https://maven.apache.org/). Herramienta que se encarga de estandarizar la estructura física de los proyectos de software, maneja dependencias (librerías) automáticamente desde repositorios y administra el flujo de vida de construcción de un software.
* [GIT](https://git-scm.com/). Sistema de control de versiones que almacena cambios sobre un archivo o un conjunto de archivos, permite recuperar versiones previas de esos archivos y permite otras cosas como el manejo de ramas (branches).
* [JUnit](https://junit.org/junit5/). Framework de Java que permite la realización de la ejecución de clases de manera controlada, para poder comprobar que los métodos realizan su cometido de forma correcta.
* [NetBeans](https://netbeans.apache.org/). Entorno de desarrollo integrado libre, orientado principalmente al desarrollo de aplicaciones Java. La plataforma NetBeans permite el desarrollo de aplicaciones estructuradas mediante un conjunto de componentes denominados “módulos”. Cada uno de estos módulos sería un archivo Java conteniendo un conjunto de clases que interactarán con las APIs de NetBeans. El objetivo de esta arquitectura es favorecer el desarrollo de funcionalidades de forma independiente y la reutilización de componentes.
* [Java](https://www.oracle.com/java/). Lenguaje de programación de propósito general, es decir, que sirve para muchas cosas, para web, servidores, aplicaciones móviles, entre otros. Java también es un lenguaje orientado a objetos, y con un fuerte tipado de variables.
* [Docker](https://www.docker.com/). Programa encargado de crear contenedores ligeros y portables para las aplicaciones software que puedan ejecutarse en cualquier máquina con Docker instalado, independientemente del sistema operativo que la máquina tenga por debajo, facilitando así también los despliegues.
* [AWS](https://aws.amazon.com/es/). Conjunto de herramientas y servicios de cloud computing de Amazon, que engloba una gran cantidad de servicios para poder realizar distintos tipos de actividades en la nube. Desde almacenamiento a la gestión de instancias, imágenes virtuales, desarrollo de aplicaciones móviles, etc.
* [CircleCI](https://circleci.com/). Plataforma moderna de integración continua y entrega continua (CI / CD) que se encarga de automatizar la construcción, pruebas e implementación de software.
[![CircleCI](https://circleci.com/gh/circleci/circleci-docs.svg?style=svg)](https://app.circleci.com/pipelines/github/Killersys/AREP-PARCIAL2T)

## Autor
[Jairo Pulido](https://github.com/Killersys)
## Licencia 
**©** Jairo Pulido, Estudiante de Ingeniería de Sistemas de la [Escuela Colombiana de Ingeniería Julio Garavito](https://www.escuelaing.edu.co/es/).

Licencia bajo la [GNU General Public License](https://github.com/Killersys/AREP-PARCIAL2T/blob/master/LICENSE).
