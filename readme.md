## Overview

This tutorial will walk you through most of technology stacks that is required for the summer internship.
followings are list materials that will be covered in this tutorial.

1. Basic Git operation
2. Fundamental of Spring Framework
3. jQuery to represent data

Once you complete each tutorial, mark your completion on this spreadsheet https://docs.google.com/spreadsheets/d/1Yxhw_C2Daihqf6XwTr_8ViK-NVN-VuDziBeMku9DyDo/edit?usp=sharing

Assignments that are X.1 is optional, but we highly recommend you complete all of the tutorial.

## Environment

Before starting this tutorial, follow the instruction below to set up your local environment.

## Download & Install tools

### Java

please download JDK from https://www.oracle.com/technetwork/java/javase/downloads/index.html

### IDE

IDE(Integrated Development Environment) supports your development.
Generally, almost all of coder are using IDE for Java development.
If you have never used any IDE, we recommend to use IntelliJ (https://www.jetbrains.com/idea/download/).
If you have already used any IDE for your development(Eclipse,IntelliJ,NetBeans, and so on), please use your favorite one :).

### Git

Git is the de-facto standard of version control system for web application development (https://git-scm.com/doc).
If you don’t know version conrtol system and git, please watch official introduction video.
And please download and install from https://git-scm.com/downloads.

### Maven

Maven is a software project manegement and comprehension tool.
You can use a lot of third party Java library from a maven repository.
Please download (https://maven.apache.org/download.cgi) and install (https://maven.apache.org/install.html) latest version.

## Hands on Tutorial

## 1. Git

You can skip this tutorial if you are already familiar with Git.
you can learn basics from [here](https://learngitbranching.js.org/).

At minimum, complete following chapters in Git Tutorial 
- Main/Introduction Sequence 1~4
- Remote/Push & Pull --Git Remotes! 1~4, 6

### 2. Accessing Data using Spring data

Spring Data JPA is used to access data from a database. Benefit of using Spring Data JPA is that you don't have to write sql to access the data. Complete the following tutorial to learn the fundamental of Spring Data.

https://spring.io/guides/gs/accessing-data-jpa/

### 2.1 Spring Data JPA advanced

- step 1: add "gender" field to Customer.java.
- step 2: In CustomerRepository.java, add an interface with two parameters, to search for first name and gender.
- step 3: in Application.java tweak the data as follows

```java
repository.save(new Customer("Jack", "Bauer"));
			repository.save(new Customer("Chloe", "O'Brian", "female"));
			repository.save(new Customer("Kim", "Bauer", "female"));
			repository.save(new Customer("David", "Palmer", "male"));
			repository.save(new Customer("Michelle", "Dessler", "female"));
```

- step 4: in Application.java, fetch the Customer whose first name is "David" and gender is "male"

### 3. Create RESTful Web Service

Firstly, read [What Are RESTful Web Services](https://docs.oracle.com/javaee/6/tutorial/doc/gijqy.html) to learn about RESTful web service and its benefit. Then, complete the following tutorial.

https://spring.io/guides/gs/rest-service/

### 3.1 Use Jackson to tweak JSON

Change the JSON response as follow, without changing field name in Greeting.java

```
{
    "user_id": 1,
    "content": "Hello, World!"
}
```

**HINT**: @JsonProperty

### 4. Consuming a RESTful Web Service with jQuery

Goal of this tutorial is to understand how to create a simple jQuery client with Spring Boot. If you can get the knowledge about jQuery, you will be able to create an UI page, which is dynamically changed.

#### Minimum requirement task

https://spring.io/guides/gs/consuming-rest-jquery/

### 4.1 Call Rakuten API with jQuery

 Try below two tasks.

1. Get the information via any Rakuten API
2. Show the information which is acquired via the Rakuten API by using jQuery.

Note: If you try to use the Rakuten API for the firts time, you need to register

#### References

[jQuery 楽天 API を必要最低限で動かす](https://qiita.com/mi-miya/items/91490004f1376c790d80)

### 5. Serving Web Content with Spring MVC

Complete below tutorial to learn how to to serve a HTML file through an endpoint. ("endpoint" means URL like 'http://localhost:8080/greeting?name=User' here)

https://spring.io/guides/gs/serving-web-content/

For your reference, the following explanation is the overview of the tutorial.

Create the pom file (for Maven)
```
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-serving-web-content</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.6.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>

    <properties>
        <java.version>1.8</java.version>
    </properties>


    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

Create a HTML file
e.g. src/main/resources/templates/greeting.html

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Serving Web Content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Hello, ' + ${name} + '!'" />
</body>
</html>
```

Create a web controller
e.g. src/main/java/hello/GreetingController.java
package hello;

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting(@RequestParam(name="name", required=false, defaultValue="World") String name, Model model) {
        model.addAttribute("name", name);
        return "greeting";
    }

}
```

Create a main java application file
e.g. src/main/java/hello/Application.java
package hello;

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Run the application with Maven (in command line)
\$ ./mvnw spring-boot:run

Test the app (input your endpoint(URL) )
<img width="353" alt="Screen Shot 2019-08-07 at 12 47 05" src="https://user-images.githubusercontent.com/7812034/62604998-2a434380-b934-11e9-9fb6-c94567705e3d.png">

### 6. Consuming a RESTful Web Service with RestTemplate

Goal of this tutorial is to understand how to consume RESTful API with Spring Boot. On Spring Boot, you can easily consume RESTful API by using "RestTemplate". If you become familiar with "RestTemplate" , you can make use of various APIs around the world.

#### Minimum requirement task

https://spring.io/guides/gs/consuming-rest/

### 6.1 Call Rakuten API with RestTemplate

Try to use any Rakuten API which you want to use and check the response.
https://webservice.rakuten.co.jp/api/simplehotelsearch/

Note: If you try to use the Rakuten API for the firts time, you need to register

---
If you want to learn about Spring Framework more in depth, I recommend these two books(Japanese)
- [Spring徹底入門](https://www.amazon.co.jp/Spring%E5%BE%B9%E5%BA%95%E5%85%A5%E9%96%80-Spring-Framework%E3%81%AB%E3%82%88%E3%82%8BJava%E3%82%A2%E3%83%97%E3%83%AA%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E9%96%8B%E7%99%BA-%E6%A0%AA%E5%BC%8F%E4%BC%9A%E7%A4%BENTT%E3%83%87%E3%83%BC%E3%82%BF/dp/4798142476/ref=sr_1_1?adgrpid=52706263349&gclid=EAIaIQobChMI6oH9paLA4gIVh3ZgCh2hAgbCEAAYASAAEgKFqvD_BwE&hvadid=338539117378&hvdev=c&hvlocphy=1009307&hvnetw=g&hvpos=1t1&hvqmt=e&hvrand=10884978008691358881&hvtargid=kwd-332386918940&hydadcr=27263_11561108&jp-ad-ap=0&keywords=spring%E5%BE%B9%E5%BA%95%E5%85%A5%E9%96%80&qid=1559116737&s=gateway&sr=8-1)
- [はじめてのSpring Boot](https://www.amazon.co.jp/%E3%81%AF%E3%81%98%E3%82%81%E3%81%A6%E3%81%AESpring-Boot%E2%80%95%E3%82%B9%E3%83%97%E3%83%AA%E3%83%B3%E3%82%B0%E3%83%BB%E3%83%95%E3%83%AC%E3%83%BC%E3%83%A0%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%A7%E7%B0%A1%E5%8D%98Java%E3%82%A2%E3%83%97%E3%83%AA%E9%96%8B%E7%99%BA-I%E3%83%BB-BOOKS-%E4%BF%8A%E6%98%8E/dp/4777519694/ref=sr_1_5?__mk_ja_JP=%E3%82%AB%E3%82%BF%E3%82%AB%E3%83%8A&keywords=spring+boot&qid=1565243460&s=gateway&sr=8-5)

If you have any question, feel free to contact us via Zoho
