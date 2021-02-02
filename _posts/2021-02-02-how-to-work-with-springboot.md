---
layout: post
title: "How to work with ... Springboot"
date: 2021-02-02
---
# How to work with ... Springboot

## Resources

### Springboot

* [Spring - Springboot](https://spring.io/projects/spring-boot)
* [Springboot Initializr](https://start.spring.io)
* [Spring Framework - Wikipedia EN](https://en.wikipedia.org/wiki/Spring_Framework)
* [Spring Framework - Wikipedia NL](https://nl.wikipedia.org/wiki/Spring_Framework)
* [A Comparison Between Spring and Spring Boot - Baeldung](https://www.baeldung.com/spring-vs-spring-boot)
* [Spring Boot Tutorial - Tutorialspoint](https://www.tutorialspoint.com/spring_boot/index.htm)
* [Spring Boot Tutorial - HowToDoInJava](https://howtodoinjava.com/spring-boot-tutorials/)
* [Spring Boot Tutorial - Java Guides](https://www.javaguides.net/p/spring-boot-tutorial.html)
* [Learn Spring Boot Tutorial - javatpoint](https://www.javatpoint.com/spring-boot-tutorial)
* [Why Spring Boot? - DZone Java](https://dzone.com/articles/why-springboot)
* [Learn Spring Boot - Baeldung](https://www.baeldung.com/spring-boot)
* [Spring Boot - Help - IntelliJ IDEA](https://www.jetbrains.com/help/idea/spring-boot.html)
* [Springboot- ZetCode](http://zetcode.com/all/#springboot)

### RESTful API

* <https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/>
* <https://dzone.com/articles/top-rest-api-best-practices>
* <https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design>
* <https://github.com/microsoft/api-guidelines>
* <https://mathieu.fenniak.net/the-api-checklist>
* <https://www.restapitutorial.com/httpstatuscodes.html>

## My related repositories

* [springboot-01-hello-world](https://github.com/PeterAnema/springboot-01-hello-world)
* [springboot-02-restful-controller](https://github.com/PeterAnema/springboot-02-restful-controller)
* [springboot-03-crud-controller](https://github.com/PeterAnema/springboot-03-crud-controller)
* [springboot-04-spring-data-jdbc](https://github.com/PeterAnema/springboot-04-spring-data-jdbc)
* [springboot-05-spring-data-jpa-customers](https://github.com/PeterAnema/springboot-05-spring-data-jpa-customers)
* [springboot-06-demo-spring-jpa-clients](https://github.com/PeterAnema/springboot-06-demo-spring-jpa-clients)
* [springboot-09-spring-security](https://github.com/PeterAnema/springboot-09-spring-security)
* [springboot-10-spring-security](https://github.com/PeterAnema/springboot-10-spring-security)
* [springboot-11-security-with-custom-users-table](https://github.com/PeterAnema/springboot-11-security-with-custom-users-table)
* [springboot-12-security-with-users-table](https://github.com/PeterAnema/springboot-12-security-with-users-table)
* [springboot-13-security-with-user-entity](https://github.com/PeterAnema/springboot-13-security-with-user-entity)
* [springboot-14-security-with-user-service](https://github.com/PeterAnema/springboot-14-security-with-user-service)
* [springboot-15-security-with-jwt](https://github.com/PeterAnema/springboot-15-security-with-jwt)
* [springboot-20-spring-https](https://github.com/PeterAnema/springboot-20-spring-https)
* [springboot-25-file-upload-basic](https://github.com/PeterAnema/springboot-25-file-upload-basic)
* [springboot-26-file-upload](https://github.com/PeterAnema/springboot-26-file-upload)
* [springboot-30-spring-boot-starter-test-assertj](https://github.com/PeterAnema/springboot-30-spring-boot-starter-test-assertj)
* [springboot-31-spring-boot-starter-test-junit-jupiter](https://github.com/PeterAnema/springboot-31-spring-boot-starter-test-junit-jupiter)
* [springboot-40-many-to-many](https://github.com/PeterAnema/springboot-40-many-to-many)
* [springboot-42-many-to-many](https://github.com/PeterAnema/springboot-42-many-to-many)
* [springboot-43-many-to-many-with-fields](https://github.com/PeterAnema/springboot-43-many-to-many-with-fields)
* [springboot-50-student-course](https://github.com/PeterAnema/springboot-50-student-course)
* [springboot-51-books-api](https://github.com/PeterAnema/springboot-51-books-api)

## Miscellaneous Comments and Snippets

### H2 in memory database

When https is enabled frames are disabled. This causes the H2 console to stop working. So you need to enable frames again to get this working. 

Add the following line to the **configure** method in the **SecurityConfig** class.

{% highlight java %}
@Configuration
@EnableWebSecurity
public class SpringSecurityConfig extends WebSecurityConfigurerAdapter {

    ...

    @Override
    protected void configure(HttpSecurity httpSecurity) throws Exception {

        ...

        httpSecurity.headers().frameOptions().disable();    // to be able to access H2 console

    }

}
{% endhighlight %}