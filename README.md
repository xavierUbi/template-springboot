# Springboot

SpringBoot es un framework de Spring que permite crear aplicaciones standalone, sin necesidad de un servidor de aplicaciones externo a ella.

Para iniciar una aplicación SB (SpringBoot a partir de ahora) bastará con ejecutar el comando "java -jar nombre_de_la_aplicacion.jar"

## Índice
1. Introducción
2. Instalación
3. Habilitación de entorno
4. Plantilla Springboot
5. Primer rest
6. Capa Persistencia Mybatis
7. Consejos
8. FAQs
9. referencias

## Introducción

[`Spring Boot`] es un framework enfocado a la creación de aplicaciones basadas en Spring sin necesidad de contenedor de aplicaciones.

A pesar de poder ejecutar aplicaciones SB en Java 17. Recuerda que el compilado se ejecuta con un entorno virtual JRE

Los requisitos para tener configurado este proyecto son:
- **Manejador de dependencias:** El control de tecnologias que estaran disponibles y configuradas en nuestro proyecto.
- **Lenguaje de programación:** Para este caso usaremos Java 17 (que para la fecha es la version LTS).
- **Framework:** El framework más usado y común y que lo usaremos es Sprinboot.
- **IDE:** Este tutorial estará configurado para que incluso lo arranques de un bloc de notas, pero habra ejemplos con Jetbrains - Idea.


**[Ir al índice](#Índice)**

## Instalación
En este ejemplo se despliegue SB con Maven 3.8.6. Se puede consultar los pasos para realizar su instalación en la siguiente dirección [http://maven.apache.org/](http://maven.apache.org/).

También se desarrollo con el kit de desarrollo opensource (OpenJdk) version 17. La misma esta disponible en la siguiente dirección [https://docs.microsoft.com/es-es/java/openjdk/download/](https://docs.microsoft.com/es-es/java/openjdk/download/).

**Spring Initializr**

Con esta página puedes crear un proyecto base de SpringBoot en la siguiente dirección [https://start.spring.io/](https://start.spring.io/).

**SpringBoot CLI**

Tanto NetBeans o Intellijent Idea tienen integrado la opción de creación de un proyecto base con SB.


**[Ir al índice](#Índice)**

## Habilitación de entorno

Se necesita configurar únicamente MAVEN_HOME y JAVA_HOME:

- **MAVEN_HOME:** Para esto solo es necesario configurarlo con el archivo binario.
- **JAVA_HOME:** Para esto solo es necesario configurarlo con el archivo binario.

En el caso de usar Eclipse entonces:
- **STS plugin:** A través del propio ide STS que se puede descargar desde el siguiente [enlace](https://spring.io/tools/sts/all) se facilita de la posibilidad al usuario para crear un proyecto base. Para ello únicamente es necesario seguir los siguientes pasos:

**[Ir al índice](#Índice)**

## Plantilla Springboot

La clase principal se compila en base al archivo principal y se puede ejecutar con el siguiente ejemplo:

```java
@SpringBootApplication
public class DemoBGApplication {
	public static void main(String[] args) {
		SpringApplication.run(DemoBGApplication.class, args);
	}
	
	@Bean 
	public String saluda(){
		System.out.println("Hola mundo...");
		return "";
	}
	
}
```

Si arrancamos de nuevo la aplicación veremos cómo aparece en los logs la frase que hemos introducido "Hola mundo...".

Para ejecutar nativamente el proyecto usa los siguientes comandos,
- **para desarrollar**:
```cmd
mvn clean install
mvn spring-boot:run
```
- **para compilar**:
```cmd
mvn clean install
java -jar SpringBootHolaMundo-0.0.1-SNAPSHOT.jar
```

**[Ir al índice](#Índice)**

## Primer rest

Para implementar un servicio rest solo es necesario crear un archivo controlador con el siguiente formato:

La clase principal se compila en el proyecto y se puede ejecutar con el siguiente ejemplo:

```java
@RestController
@MapperScan("bg.com.bo.demoBG.dao")
public class TestController {

    @Autowired
	private ACHService achServicio;

    @GetMapping("/test")
    public ResponseEntity<String> test(){
        return new ResponseEntity<String>("Hola mundo!!", HttpStatus.OK);
    }
}
```
y si lo ejecutamos con os comandos mencionados sale:

<p align="center"><img src="https://raw.githubusercontent.com/javiercode/demoBG/main/src/main/resources/assets/holaMundo.png"></p>

**[Ir al índice](#Índice)**


## Consejos
En el siguiente apartado se han recopilado distintos consejos obtenidos con la experiencia a la hora de realizar desarrollos mediante el framework de SB:
### Estructura de un proyecto SB
La estructuración típica de los ficheros de una aplicación SB con distintas capas se definirá siguiendo la siguiente nomenclatura de paquetes:
```xml
└── src/main/java
    └── bg.com.bo.demoBG
        └── DemoBgApplication.java
    └── web/
        └── TestController.java
```

Para agreagar swwager solo añada la siguientes dependencias del siguiente [enlace](https://www.baeldung.com/spring-rest-openapi-documentation)

- Añada la dependencia de documentacion:
```xml
<dependency>
  <groupId>org.springdoc</groupId>
  <artifactId>springdoc-openapi-ui</artifactId>
  <version>1.6.4</version>
</dependency>
```
- Se podrá ver la documentacion asi:
<p align="center"><img src="https://raw.githubusercontent.com/javiercode/demoBG/main/src/main/resources/assets/api-docs.png"></p>
- Tambien se podra ver el resultado asi:

Se puede acceder al SWAGGER desde el siguiente [enlace](http://localhost:8080/demo-bg/api/swagger-ui/index.html).
<p align="center"><img src="https://raw.githubusercontent.com/javiercode/demoBG/main/src/main/resources/assets/swagger.png"></p>

**[Ir al índice](#Índice)**
## FAQs
### ¿Qué es Spring Boot?
**[Ir a la descripción](#introducci%C3%B3n)**
### ¿Qué ventajas aporta Spring Boot?
- Reduce el el tiempo y esfuerzo en el desarrollo y testeo de aplicaciones.
- El uso de JavaConfig ayuda en lugar del uso de XMLs.
- Reduce el número de librerías necesarias y los conflictos entre versiones.
- Rapided en el inicio del desarrollo gracias a las configuraciones por defecto.
- No es necesario de un servidor web independiente.
- Menos configuración necesaria gracias a la @Configuration.
- El uso de perfiles (profiles) facilita el uso de configuración por entorno.
### ¿Qué herramientas de construcción de proyectos se pueden utilizar para desarrollar una aplicación Spring Boot?
- Maven
- Gradle
### ¿Qué es JavaConfig?
Es un producto de Spring que facilita la posibilidad de realizar la configuración de la aplicación en lenguaje JAVA en lugar de mediante ficheros XML de configuración.
Sus ventajas son:
- Orientación a objetos de configuración (herencia, ...)
- Reduce o elimina la configuración por XML y sus problemas en la codificación.
- Reduce los problemas derivados de la codificación errónea de los tipos de datos en los XML.
### ¿Cómo se puede configurar una aplicación Spring Boot para que se redesplieguen los cambios automáticamente?
Mediante el uso de DevTools:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
</dependency>
```
### ¿Qué papel juega el Actuator de Spring Boot?
**[Ir a la descripción](#springboot-actuator)**
### ¿Cómo se puede modificar el puerto de una aplicación Spring Boot?
Incluyendo la propiedad **server.port=8090** en el fichero application.properties.
### ¿Qué es el YAML?
**[Ir a la descripción](#yaml-como-fichero-de-configuraci%C3%B3n)**
### ¿Cómo se puede agregar una capa de seguridad a una aplicación de Spring Boot?
Mediante el uso del starter **spring-boot-starter-security** y agregando la configuración de seguridad adecuada.
### ¿Cómo se puede integrar Spring Boot y ActiveMQ?
Mediante el uso del starter **spring-boot-starter-activemq** y la configuración de acceso al gestor de colas apropiada.
### ¿Cómo se puede integrar Spring Boot y Kafka?
Mediante el uso de la dependencia **spring-kafka** y la configuración de acceso al gestor de colas apropiada.
### ¿Cómo se puede implementar la paginación y ordenación en Spring Boot?
Se pueden crear servicios paginados y ordenados en las aplicaciones Spring Boot mediante el uso de los CrudRepository que exponen mediante servicios REST el modelo de datos asociado.
### ¿Qué es swagger? ¿Qué papel juega en una aplicación Spring Boot?
Swagger es un estándar de desarrollo de APIs que permiten realizar la representación visual completa de servicios RESTful.
### ¿Qué son los perfiles en Spring? ¿Para qué se utilizan?
Los perfiles de Spring permiten a los desarrolladores registrar diferentes beans dependiento del perfil en el que se encuentren.
### ¿Qué es Spring Batch y cómo se integra con una aplicación Spring Boot?
**[Ir a la descripción](#spring-batch)**
### ¿Qué es un template de FreeMarker?
Es un genérador de código basado en java enfocado en la generación de la capa de presentación de una aplicación con modelo MVC.
### ¿Qué es el cacheo? ¿Cómo puede cachearse información en Spring Boot?
La acción de cachear información consiste en almacenar en memoria local cierta información que se accede con alta frecuencia para reducir costes computacionales o de red altos. Un framework de cacheo extendido puede ser Hazelcast.
### ¿Qué es Apache Kafka?
Apache Kafka es un sistema de mensajería basado en el patrón publicador/suscriptor. Entre sus principales características destacan:
- Escalable
- Tolerante a fallos
- Publicador - Suscriptor
### ¿Qué componentes de Spring Cloud existen?
Algunos de los principales componentes que forman Spring Cloud son:
- Eureka
- Zuul
- Config Server
- Ribbon
  **[Ir al índice](#Índice)**
## Referencias
* [Spring Boot - Reference Documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
* [Spring Boot in Action](https://doc.lagout.org/programmation/Spring%20Boot%20in%20Action.pdf)
* [Spring Boot Learn by examples](http://samples.leanpub.com/springboot-learn-by-example-sample.pdf)
* [Ejemplos de Spring Boot](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples)
  **[Ir al índice](#Índice)**