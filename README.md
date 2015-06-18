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


## Opciones de depuración


