# Spring Workshop 5.0 version
## Big Picture of Spring Framework
* Flexible and modular Architecture with No restrictions e.g.segregated web, business and data layer. No restrictions as i can still use struts or hibernate or any other framework while using spring. or it provides AOP module but i am free to integrate with AspectJ for more features which is a AOP framework
* Design — Very loosely coupled and spring defacto promotes loose coupling. This helps in ease of unit testing or even creating autonomous services.
* Code — Easy to unit Test
* Features — Dependency injection, IOC (bean factory and Application context) container, auto wiring, component scan
* Spring modules : Spring is modular framework having core container, data layer, web layer and many other modular frameworks
* Spring projects: Spring provides spring projects for specific needs like spring boot, spring cloud, spring Data, Spring Integration, Spring batch, spring security, spring HATEOAS and many other spring Projects.


## Spring Modules
* Core container: Beans, Core, Context, SpEL
* Data Access/Integation Layer: JDBC, ORM, OXM, JMS, Transactions
* Web: Websocket, Servlet, Web, Portlet
* Other: AOP, Aspects, Instrumentation, Messaging, Test

Note: All these modules share the same version of spring framework

## Spring Projects
* Spring boot project: Quickly build applications using autoconfiguration, actuator, start up projects, makes micro services development a cake walk.
* Spring cloud: Build cloud native apps that are dynamically deploy able, configurable to cloud.
* Spring Data: Consistent data access to connect to a mix of data sources like SQL or no-SQL database.
* Spring Integration: Makes application integration very easy and follows the enterprise integration patterns.
* Spring Batch: For batch features
* Spring Security: For securing your applications like your REST service or web application
* Spring HATEOAS: Provides way for implementing HATEOAS rest services.
* Others: Spring session, Spring mobile, Spring web services etc

## Spring versions and new features
* Spring 2.5 → Annotation configuration
* Spring 3.0 → Use of Java 5 improvements
* Spring 4.0 → First version with full support of Java 8 features. Minimum version to be used with Spring 4.0 is Java 6. Introduction of @RestController annotation. Spring 4.1 supported JCache(JSR-107) annotations
* Spring 5.0

→ Functional Web framework

→ Support for Jigsaw(Java modularity): Size of xurrent java installation is ~150 MB which is big considering IoT devices or other thin platforms, Jigsaw is a attempt to make Java modular by reducing the size by virtue of making java virtual.

→ Support for reactive programming: Reactive programming emphasizes of use of events and application reacting to events

→ Support for Kotlin: Kotlin is a evolving application and the same java code can be written in much less lines.

## Design Patterns in Spring
* Front Controller — Dispatcher servlet. Any request coming from the client/browser will first go to the dispatcher servlet and will only then be redirected to other controllers
* Prototype — Beans creation
* Dependency Pattern — Dependency injection
* Factory Pattern — Bean factory and application context
* Template method — Examples like Abstract Controller or JDBC Tempate or REST Template
## IOC Container
* Find the beans (by @Component)
* Identify dependencies(by @Autowire)
* Manage lifecycle of a bean

Bean factory — Basic container management capabilities as mentioned above

Application Context: Bean factory+ AOP featues + I18N featues + web application context for web applications.

We use @configuration to define a application context using java

To create a application context in unit tests, we use @runwith(SpringJUnit4ClassRunner.class) annotation followed by @ContextConfiguration(Classes=<Classname.class>)

Recommendation between Application context and Bean Factory: Use application context for most situations except when you are in severe memory constraint and internationalization, AOP or Web features are not required.

Component Scan: This is a search done by spring for component. We define the base packages to control where spring should do the search.

In Springboot we use the annotation @SpringbootApplication or @SpringBootTest and they automatically initiate a component scan in the package(and subpackages) where they are defined.

## 5 Most popular annotations in Spring
* @component: Spring should manage this class as a generic bean
* @autowired: Spring should find a matching bean and wire the dependency
* @Repository: Used on a DAO, and related to getting the data from your database. Encapsulates Storage, retrieval, and search behavior typically from a relational database. It takes care of exception translation from JDBC exceptions to Spring exceptions
* @Service: Business service facade
* @Controller: Controller in MVC pattern
## The 4 Bean scopes in Spring
* Singleton: One instance per spring context. This is the default scope.
Note for singleton: If you have multiple spring context in a JVM, you will have multiple singleton instances per spring context. This is the slight different singleton pattern compared to the GoF pattern definition.
* prototype: New bean whenever requested
request: One bean per http request. Web-aware spring application context
* session: One bean per http session. Web-aware spring application context

Thread-safety of beans: By default spring beans are not thread safe as the default scope is singleton.

## Setter Injection, Constructor Injection and the third way
* Setter injection: This happens via the setter we provide with @autowired annotation. We use setter injection for optional dependencies. Setter injection leads to change the state of the bean and hence bean isnt immutable and hence spring doesnt advocate this over constructor injection.
* Constructor injection: This happens via the constructor we provide with @autowired annotation. Spring advocates using Constructor injection. We use constructor injection for mandatory dependencies. Advantage — Entire bean is created in one instance. This makes the dependency a immutable bean. Downside, to many constructor injections leads to poor code, that’s a candidate for refactoring and poor readability.
* Third way: Directly putting @Autowired on the dependency bean instead of its constructor or method. Here, Spring uses reflection for the wiring, and this works as a setter injection internally.

## Autowiring in Spring
* By type — Specifies autowiting by property type. Spring container looks at the beans on which autowire attribute is set to byType. It then tries to match and wire a property if its type matches with exactly one of the beans name in the configuration file.
* By name — Spring Autowiring ‘byName’ specifies autowiring by property name. Spring container looks at the beans on which auto-wire attribute is set and on finding more then one dependencies checks the reference name matching. It then tries to match and wire its properties with the beans defined by the same names in the configuration file.
* constuctor — similar to byType, but through constructor

## Typical Spring Exceptions
* NoUniqueBeanDefinitionException: When spring finds more than one matching bean. This can be solved by using annotation @ Primary or the other option is to use @Qualifier (“dependent bean name”)
* NoSuchBeanDefinitionException: When the dependent beans dont have component written on them or the component scan base package declaration isn’t done well. The error also comes as No qualifying bean of type …. found.

## CDI (Contexts and Dependency Injection)
* Java EE dependency injection standard(JSR-330)
* Spring supports most annotations like @inject (Autowired), @Named (@component and @qualifier) and singleton (to define scope of a bean)
BOM in Spring

## Simplest way to ensure that we are using the same version of all spring related dependencies. BOM is abbrevation for Bill Of Materials.
<dependencyManagement>
<dependencies>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-framework-bom</artifactId>
<version>5.0.0.RELEASE</version>
<type>pom</type>
<scope>import</scope>
</dependency>
</dependencies>
</dependencyManagement>
