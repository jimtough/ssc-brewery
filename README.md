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

## recommended references

* Documentation on Security Filter implementations we can use
  * https://docs.spring.io/spring-security/site/docs/current/reference/html5/#servlet-security-filters

## configuration

* Take a look at the `SecurityConfig` class under the 'config' package
  * Note the `@EnableWebSecurity` annotation
  * Note that we are extending `WebSecurityConfigurerAdapter`
    * Instructor recommends looking at the Spring implementation of this class and get familiar with the default behaviour of its methods
    * It is common practice to override individual methods of `WebSecurityConfigurerAdapter` in your application 
  * Matcher types in `SecurityConfig`
    * Ant Matcher type uses * or ** wildcards
    * MVC Matcher type uses path parameters in Spring MVC syntax (example: {upc})
  * You can configure your own in-memory store of users/roles with `UserDetailsService` and `InMemoryUserDetailsManager` for testing and demos (not typically used for production)
* TIP: As your project gets more complex, method-level security can be easier to manage than configuring global-level security (as in `SecurityConfig.configure()`)
  * The @PreAuthorize method-level security annotation, used with a 'hasAuthority()' SPeL expression allows for a very fine-grained permissions setup that is easy to maintain
* Spring Security JPA allows you to mix SPeL (to do authority checks) in with JPQL query language
* To enable Spring Security JPA features, you must do the following:
  * Add the POM dependency
  * Declare a `SecurityEvaluationContextExtension` bean in your context (in a @Configuration class typically)
* Spring Security provides a tag library for JSP and Thymeleaf templates
  * requires a Spring Security 5 Thymeleaf extras dependency in your project
  * each Thymeleaf template page must have a namespace declaration for the tag library
* 'Remember Me' with persistent tokens requires an application database and specific table structure
  * Instructor demonstrates how to set this up in one of the lectures

## troubleshooting

* Use the 'Inspect' tool in Chrome to view problems when pages or page elements will not load (check 'Network' tab)

## miscellaneous

* The instructor's example project requires a `mvn package` before running if you want to see all the CSS styling (depends on a Maven plugin)
* Adding the 'spring-boot-starter-security' starter will automatically enable the following:
  * Basic authentication, with username 'user' and an randomly generated password that will appear in the console log
  * Simple login and logout pages in the application with built-in styling
* The default basic auth username and password can be overridden with these properties:
  * `spring.security.user.name`
  * `spring.security.user.password`
* In test `BeerControllerIT`:
  * `@WithMockUser("spring")` will bypass authentication and force the test to run with authenticated user 'spring' in the request
  * `findBeersWithHttpBasic()` will actually do basic authentication against user 'spring' with password 'guru'
* Instructor suggests copying either methods from `AbstractAuthenticationProcessingFilter` and pasting a modified version into your own implementation, when you are creating a custom filter.
  * example: `RestHeaderAuthFilter` - Copy overridden method, then delete code that isn't relevant to a REST service method (like 'remember me' stuff)
* If you only implement one `UserDetailsService` bean in your application, then Spring will use it by default
* Remember that @Transactional causes Spring to start/end a database transaction at the entry/exit point of the annotated method
  * This may be a better solution than declaring your JPA entity relationships to be 'eager fetch'
* Take a look at the example of a @Nested test in `BeerRestControllerIT` - good way to segregate a destructive database operation in an integration test
  * In subsequent lectures the instructor has added more great examples of @Nested and @Parameterized tests that help keep things organized
* SecurityContextHolder - Instructor uses this in places where the `SecurityContext` object is not available
  * DESCRIPTION FROM SPRING SECURITY DOCS: ...The most fundamental object is SecurityContextHolder . This is where we store details of the present security context of the application, which includes details of the principal currently using the application. By default the SecurityContextHolder uses a ThreadLocal to store these details, which means that the security context is always available to methods in the same thread of execution, even if the security context is not explicitly passed around as an argument to those methods. Using a ThreadLocal in this way is quite safe if care is taken to clear the thread after the present principal’s request is processed. Of course, Spring Security takes care of this for you automatically so there is no need to worry about it.
  * REFERENCE: https://www.docs4dev.com/docs/en/spring-security/5.1.2.RELEASE/reference/overall-architecture.html
