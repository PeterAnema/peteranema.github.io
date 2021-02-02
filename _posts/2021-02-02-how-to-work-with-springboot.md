# How to work with ... Springboot

## Resources


## My repositories


## Miscellaneous Comments and Snippets

### H2 in memory database

When https is enabled frames are disabled. This causes the H2 console to stop working. So you need to enable frames again to get this working. Add the following line to the **configure** method in the **SecurityConfig** class.

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