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