# Brewery Spring MVC Monolith

This repository contains source code examples used to support my on-line courses about the Spring Framework.

You can learn more about the courses here:
* [Spring Security Core: Beginner to Guru](https://www.udemy.com/course/spring-security-core-beginner-to-guru/?referralCode=306F288EB78688C0F3BC)
* [Spring Boot Microservices with Spring Cloud](https://www.udemy.com/course/spring-boot-microservices-with-spring-cloud-beginner-to-guru/?referralCode=6142D427AE53031FEF38)
* [Spring Framework 5: Beginner to Guru](https://www.udemy.com/course/spring-framework-5-beginner-to-guru/?referralCode=6D9ECD1F93988FEE5CE9)
* [Testing Spring Boot: Beginner to Guru](https://www.udemy.com/course/testing-spring-boot-beginner-to-guru/?referralCode=EFFE87DDE96C8541B2EE)
* [Apache Maven: Beginner to Guru](https://www.udemy.com/course/apache-maven-beginner-to-guru/?referralCode=0B91047D034706031F51)

----

# My own notes (Jim Tough)  :)

## miscellaneous

* Adding the 'spring-boot-starter-security' starter will automatically enable the following:
  * Basic authentication, with username 'user' and an randomly generated password that will appear in the console log
  * Simple login and logout pages in the application with built-in styling
* The default basic auth username and password can be overridden with these properties:
  * `spring.security.user.name`
  * `spring.security.user.password`
