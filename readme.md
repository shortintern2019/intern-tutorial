## Overview
This tutorial will walk you through most of technology stacks that is required for the summer internship.
followings are list material that will be coverd in this tutorial. 
1. Basic Git operation
2. Fundamental of Spring Framework
3. Jquery to represent data

Once you complete each tutorial, mark your completion on this spreadsheet https://docs.google.com/spreadsheets/d/1Yxhw_C2Daihqf6XwTr_8ViK-NVN-VuDziBeMku9DyDo/edit?usp=sharing

 Assignments that are X.1 is optional, but we highly recommend you complete all of the tutorial.
 
## Environment
before starting this tutorial, follow the instruction below to set up your environment.
Environment

## Download & Install tools

### Java
please download jdk(Java Development Kit) from https://www.oracle.com/technetwork/java/javase/downloads/index.html

### IDE
IDE(Integrated Development Environment) supports your development.
Generally, almost all of coder are using IDE for Java development.
If you have never been to use any IDE, we recommend to use IntelliJ (https://www.jetbrains.com/idea/download/).
If you have already used any IDE for your development(Eclipse,IntelliJ,NetBeans, and so on), please use your favorite one :).

### Git
Git is the de-facto standard of version control system for web application development (https://git-scm.com/doc).
If you don’t know version conrtol system and git, please watch official introduction video.
And please download and install from https://git-scm.com/downloads.

### Maven
Maven is a software project manegement and comprehension tool.
You can use a lot of third party Java library from a maven repository.
Please download (https://maven.apache.org/download.cgi) and install (https://maven.apache.org/install.html) latest version.

### Editor
If you don’t use any editor for developer, we strongly recommend to install the editor.
For example Atom (https://atom.io/) is an editor by GitHub.

## Hands on Tutorial

## 1. Git
Git is the de-facto standard of version control system for web application development. You can skip this tutorial if you are already familiar with Git.
you can learn basics from [here](https://learngitbranching.js.org/).

## Spring Framework Tutorial
For Spring Frame Tutorial, create a new branch from the master branch. Branch name should be in format of "feature/FIRSTNAME_LASTNAME". Once you complete the tutorial push your work to the GitHub repository.


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

### 3.1 Use Jackson to tweak Json
Change the Json response as follow, without changing field name in Greeting.java
```
{
    "user_id": 1,
    "content": "Hello, World!"
}
```
**HINT**: @JsonProperty

### 4. Consuming a RESTful Web Service with jQuery
This tutorial is aiming to understand how to create a simple jQuery client with Spring Boot. If you can get the knowledge about jQuery, you become able to create an UI page, which is dynamically changed.

#### Minimum requirement task
https://spring.io/guides/gs/consuming-rest-jquery/

### 4.1 Call Rakuten API with jQuery
You try below two task.

1. Get the information via the Rakuten API
2. Show the information which is aquired via the Rakuten API by using jQuery.


#### References
[jQuery 楽天 API を必要最低限で動かす](https://qiita.com/mi-miya/items/91490004f1376c790d80)

### 5. Serving Web Content with Spring MVC

#### purpose

To be able to get your HTML file from an endpoint. ("endpoint" means URL like 'http://localhost:8080/greeting?name=User' here)

#### to do
Let's try this tutorial (https://spring.io/guides/gs/serving-web-content/) !!


For your reference, the following explanation is the overview of the tutorial. 

Create a pom file (for Maven)
e.g. pom.xml

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
This tutorial is aiming to understand how to use RESTful API with Spring Boot. On Spring Boot, you can easily use RESTful API by using "RestTemplate". If you become able to use "RestTemplate" perfectly, you can realize various idea that you think.

#### Minimum requirement task
https://spring.io/guides/gs/consuming-rest/

### 6.1 Call Rakuten API with RestTemplate
You try to use the Rakuten API which you want to use and check the response.
https://webservice.rakuten.co.jp/api/simplehotelsearch/

Note: If you try to use the Rakuten API for the firts time, you need to register 
