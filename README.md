# GradleTomcat
El principal fin de este tutorial es presenta, paso a paso, un ejemplo básico para desplegar una aplicación en Tomcat mediante gradle, utilizando el plugin https://github.com/bmuschko/gradle-tomcat-plugin .

## Paso 1. Definición de los fuentes del plugin
Los fuentes están disponibles en Bintray.

```
buildscript {
    repositories {
        jcenter()
    }

    dependencies {
        classpath 'com.bmuschko:gradle-tomcat-plugin:2.2.2'
    }
}
```

## Paso 2. Uso del plugin
Indicamos que vamos a utilizar el plugin com.bmuschko.tomcat. Dicho plugin proporciona tareas para iniciar y parar un contenedor Tomcat embebido y exponer la extensión 'Tomcat'.

```
apply plugin: 'com.bmuschko.tomcat'
```

## Paso 3. Dependencias
Además es necesario incluir una serie de dependencias de tomcat.  En nuestro caso vamos a utilizar la versión 7.0.61.

```
    def tomcatVersion = '7.0.61'
    tomcat "org.apache.tomcat.embed:tomcat-embed-core:${tomcatVersion}",
            "org.apache.tomcat.embed:tomcat-embed-logging-juli:${tomcatVersion}",
            "org.apache.tomcat.embed:tomcat-embed-jasper:${tomcatVersion}"
```

## Ejemplo completo
El siguiente es un ejemplo que se vale del plugin 'com.bmuschko.tomcat' para desplegar un contenedor embebido de tomcat.

```
group 'es.kestrel.labs'
version '1.0-SNAPSHOT'

apply plugin: 'java'
apply plugin: 'war'
apply plugin: 'idea'
apply plugin: 'com.bmuschko.tomcat'

sourceCompatibility = 1.5

repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
}

dependencies {
    def tomcatVersion = '7.0.61'
    tomcat "org.apache.tomcat.embed:tomcat-embed-core:${tomcatVersion}",
            "org.apache.tomcat.embed:tomcat-embed-logging-juli:${tomcatVersion}",
            "org.apache.tomcat.embed:tomcat-embed-jasper:${tomcatVersion}"


    compile "javax.ws.rs:jsr311-api:1.1.1"

    compile 'com.sun.jersey:jersey-server:1.19'
    compile 'com.sun.jersey:jersey-core:1.19'
    compile 'com.sun.jersey:jersey-servlet:1.19'
    compile 'com.sun.jersey:jersey-json:1.19'
    compile 'org.hibernate:hibernate-core:3.6.0.Final'
    compile 'javax.servlet:javax.servlet-api:3.1.0'
    compile 'mysql:mysql-connector-java:5.1.35'
    compile 'org.slf4j:slf4j-simple:1.7.12'
    compile 'org.javassist:javassist:3.19.0-GA'
    compile 'org.hibernate:hibernate-c3p0:3.6.0.Final'
    compile name: 'MonitorizadorComun'
    testCompile group: 'junit', name: 'junit', version: '4.11'
}

buildscript {
    repositories {
        jcenter()
    }

    dependencies {
        classpath 'com.bmuschko:gradle-tomcat-plugin:2.2.2'
    }
}
```

## Paso 4. Ejecución
Para realizar el despliegue de la aplicación podemos ejecutar los siguientes comandos:
--> Despliegue war

```
gradle tomcatRunWar
```

--> Despliegue de los ficheros

```
gradle tomcatRun
```

--> Si queremos ver las tareas disponibles

```
gradle tasks
```

## Opciones de depuración (IntelliJ)
1.Para desplegar la aplicación en modo de depuración, debemos crear una variable de entorno.

```
GRADLE_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005"
```

2.Asociar el depurador de nuestro entorno a la aplicación. Desde IntelliJ accedemos al menu Run -> Edit Configurations...

3.Creamos una nueva configuración de tipo Remote.
    
    3.1. Seleccionamos la opción 'Socket' para 'Transport'.

    3.2. Seleccionamos la opción 'Attach' para 'Debugger mode'.

    3.3. Host -> localhost

    3.4. Port -> 5005

