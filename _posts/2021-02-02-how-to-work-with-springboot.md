---
layout: post
title: "How to work with ... Springboot"
description: "Tips and tricks for working with Springboot"
date: 2021-02-02
category: Dev
tags: [Web, Springboot, Java]
---

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

{%- for repository in site.github.public_repositories -%}
{% if repository.name | split: "-" | first == "springboot" %}
* [{{ repository.name }}]({{ repository.html_url }})
{%- endif -%}
{%- endfor -%}
{% %}

## Miscellaneous Comments and Snippets

### H2 in memory database in combination with https

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