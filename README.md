Spring Boot with Docker
This guide walks you through the process of building a Docker image for running a Spring Boot application. We start with a basic Dockerfile and make a few tweaks. Then we show a couple of options that use build plugins (for Maven and Gradle) instead of docker. This is a "getting started" guide, so the scope is limited to a few basic needs. If you are building container images for production use there are many things to consider and it is not possible to cover them all in a short guide.

There is also a Topical Guide on Docker, which covers a wider range of choices that we have here, and in much more detail.
What you’ll build
Docker is a Linux container management toolkit with a "social" aspect, allowing users to publish container images and consume those published by others. A Docker image is a recipe for running a containerized process, and in this guide we will build one for a simple Spring boot application.

What you’ll need
About 15 minutes

A favorite text editor or IDE

JDK 1.8 or later

Gradle 4+ or Maven 3.2+

You can also import the code straight into your IDE:

Spring Tool Suite (STS)

IntelliJ IDEA

If you are NOT using a Linux machine, you will need a virtualized server. By installing VirtualBox, other tools like the Mac’s boot2docker, can seamlessly manage it for you. Visit VirtualBox’s download site and pick the version for your machine. Download and install. Don’t worry about actually running it.

You will also need Docker, which only runs on 64-bit machines. See https://docs.docker.com/installation/#installation for details on setting Docker up for your machine. Before proceeding further, verify you can run docker commands from the shell. If you are using boot2docker you need to run that first.

How to complete this guide
Like most Spring Getting Started guides, you can start from scratch and complete each step or you can bypass basic setup steps that are already familiar to you. Either way, you end up with working code.


Download and unzip the source repository for this guide, or clone it using Git:
cd into 
Jump ahead to Set up a Spring Boot app.

The Spring Boot Maven plugin provides many convenient features:

It collects all the jars on the classpath and builds a single, runnable "über-jar", which makes it more convenient to execute and transport your service.

It searches for the public static void main() method to flag as a runnable class.

It provides a built-in dependency resolver that sets the version number to match Spring Boot dependencies. You can override any version you wish, but it will default to Boot’s chosen set of versions.

    ./mvnw package

Containerize It

Docker has a simple "Dockerfile" file format that it uses to specify the "layers" of an image. 

So let’s go ahead and create a Dockerfile in our Spring Boot project:

Dockerfile

    FROM openjdk:8-jdk-alpine
    ARG JAR_FILE=target/*.jar
    COPY ${JAR_FILE} app.jar
    ENTRYPOINT ["java","-jar","/app.jar"]COPY
    
 You can run it (if you are using Maven) with
 
    docker build -t
    java -jar target/*.jar
    
    
