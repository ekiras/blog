---
layout: post
title: How to use & configure SessionFactory Bean
tags: SessionFactory SpringBoot
redirect_from: "/2016/02/how-to-use-configure-session-factory-bean-springboot.html"
---

## Points To Remember
* Add the <b>SessionFactory</b>&nbsp;bean in the Application class.
* Add the Current Session Context class in application.properties.
* Use the SessionFactory using&nbsp;<b>@Autowired</b>&nbsp;annotation.
    
    
    
## How to Configure &amp; Use SessionFactory Bean

Add the following to the Main Application class or Configuration class.  

```
@Bean  
public SessionFactory sessionFactory(HibernateEntityManagerFactory hemf){ 
    return hemf.getSessionFactory();  
}
```
 
Add the following line in application.properties  
```
spring.jpa.properties.hibernate.current_session_context_class=org.springframework.orm.hibernate4.SpringSessionContext
```
Now you can use the Session Factory in your code as follows.
```
class Sample {
      @Autowired SessionFactory sessionFactory; 
      // use sessionFactory.getCurrentSession(); to get the current session 
}
```
