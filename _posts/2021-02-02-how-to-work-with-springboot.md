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
{% if repository.name contains "springboot" or repository.topics contains "springboot" %}
  * [{{ repository.name }}]({{ repository.html_url }})
{%- endif -%}
{%- endfor %}

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

### Jackson helper is used to serialize and deserialize objects to JSON

Annotations:
* @JsonIgnore
* @JsonIgnoreProperties
* @JsonView
* @JsonProperty
* @JsonBackReference
* @JsonManagedReference

{% highlight java %}
@Entity
public class Book{  
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column
    private String title;

    @Column
    private String description;

    @ManyToMany(cascade = CascadeType.ALL)
    @JoinTable(name = "book_author", 
               joinColumns = @JoinColumn(name = "book_id", referencedColumnName = "id"),
               inverseJoinColumns = @JoinColumn(name = "author_id", referencedColumnName = "id"))
    @JsonIgnoreProperties("books")
    private Set<Author> authors;
}

@Entity
public class Author {  
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column
    private String name;

    @ManyToMany(mappedBy = "authors")
    @JsonIgnoreProperties("authors")
    private Set<Book> books;
}
{% endhighlight %}


#### Links
* https://www.baeldung.com/jackson-bidirectional-relationships-and-infinite-recursion
* https://hellokoding.com/handling-circular-reference-of-jpa-hibernate-bidirectional-entity-relationships-with-jackson-jsonignoreproperties/


## Cross-Origin Resource Sharing (CORS)

In many cases, the host that serves the JS (e.g., example.com) is different from the host that serves the data (e.g., api.example.com). In such a case, CORS enables cross-domain communication.


For example, your web application is running on 8080 port and by using JavaScript you are trying to consuming RESTful web services from 9090 port. Under such situations, you will face the Cross-Origin Resource Sharing security issue on your web browsers.

Spring provides first-class support for CORS, offering an easy and powerful way of configuring it in any Spring or Spring Boot web application.

Two requirements are needed to handle this issue
* RESTful web services should support the Cross-Origin Resource Sharing.
* RESTful web service application should allow accessing the API(s) from the 8080 port.

### Set the origins for RESTful web service with the @CrossOrigin annotation.

{% highlight java %}
@CrossOrigin(origins = ..., 
             methods = ..., 
             allowedHeaders = ..., 
             exposedHeaders = ..., 
             allowCredentials = ..., 
             maxAge = ...)
{% endhighlight %}

Per controller method by:

{% highlight java %}
@RequestMapping(value = "/products")    # no value specifies all origins allowed
@CrossOrigin(origins = "http://localhost:8080")
public ResponseEntity<Object> getProduct() {
   return null;
}
{% endhighlight %}

Or per controller by:

{% highlight java %}
@CrossOrigin(origins = "http://example.com", maxAge = 3600)
{% endhighlight %}

Or globally

{% highlight java %}
@Configuration
public class AppConf implements WebMvcConfigurer {
   return new WebMvcConfigurerAdapter() {
      @Override
      public void addCorsMappings(CorsRegistry registry) {
         registry.addMapping("/products").allowedOrigins("http://localhost:9000");
      }    
   };
}
{% endhighlight %}

### In combination with our Spring Security.

If we use the Spring Security in our project, we must take an extra step to make sure it plays well with CORS. It's because CORS must be processed first. Otherwise, Spring Security will reject the request before it reaches Spring MVC.

{% highlight java %}
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.cors().and()...
    }
}
{% endhighlight %}

### Links
* https://www.tutorialspoint.com/spring_boot/spring_boot_cors_support.htm
* https://www.baeldung.com/spring-cors
* https://zetcode.com/springboot/cors/
* https://www.javadevjournal.com/spring-boot/spring-boot-cors/
* https://howtodoinjava.com/spring5/webmvc/spring-mvc-cors-configuration/#global-cors
* https://medium.com/@dtkatz/3-ways-to-fix-the-cors-error-and-how-access-control-allow-origin-works-d97d55946d9
* https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-cors
