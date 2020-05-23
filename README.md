# Netflix-zuul-gateway

Netflix Zuul API Gateway : Zuul is the front door for all requests from devices and web sites to the backend of the Netflix streaming application. As an edge service application, Zuul is built to enable dynamic routing, monitoring, resiliency and security

# What is the Netflix Zuul? Need for it?

Zuul is a JVM based router and server side load balancer by Netflix.
It provides a single entry to our system, which allows a browser, mobile app, or other user interface to consume services from multiple hosts without managing cross-origin resource sharing (CORS) and authentication for each one. We can integrate Zuul with other Netflix projects like Hystrix for fault tolerance and Eureka for service discovery, or use it to manage routing rules, filters, and load balancing across your system.

* Microservice call without Netflix Zuul

![alt text](https://www.javainuse.com/boot-25_1.jpg)

* Microservice call with Netflix Zuul

![alt text](https://www.javainuse.com/boot-25_2.jpg)

* Microservice call with Netflix Zuul + Netflix Eureka

![alt text](https://www.javainuse.com/boot-25_3.jpg)

# Tech Stack

* Spring Boot
* Netflix Zuul
* Maven

# Maven Dependencies

```
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>
```

# Entries in Application.yml

```
eureka:
    client:
        serviceUrl:
            defaultZone: http://localhost:8083/eureka
server:
    port: 8085
    
zuul:
    ignoredServices: '*'
    host:
        max-total-connections: 100
        max-per-route-connections: 100
    routes:
        ## By default, all requests to producer service for example will start with: "/producer/"
        ## What will be sent to the producer service is what comes after the path defined,
        ## So, if request is "/producer/employee", producer service will get "/employee".
        employee-producer:
            path: /producer/**
            service-id: EMPLOYEE-PRODUCER
        Spring-Boot-REST-Hibernate-PostgreSql-CRUD:
            path: /empdetails/**
            serviceId: SPRING-BOOT-REST-HIBERNATE-POSTGRESQL-CRUD

spring:
    application:
            name: netflix-zuul-gateway    
```
