# SpringInAction

## Spring annotations

### @Component
This simple annotation identifies the class as a component class and serves as a clue to Spring that a bean should be created for the class.

### @ComponentScan
Enables spring scan in the package and all the subpackeges, looking for classes annotated with @Component.

### SpringBootApplication

This is actually a composite that combines three other annotations:

1. @SpringBootConfiguration - this is a specialized form of the @Configuration annotation and it tells to the Spring context that this class has some configurations it should manage(beans)

2. @EnableAutoConfiguration - Enables spring automatic configuration. It looks on the classpath for frameworks and defined beans. It's actually trying to guess what beans you need to be configured and managed for your application.
Auto-configuration tries to be as intelligent as possible and will back-away as you define more of your own configuration. You can always manually exclude() any configuration that you never want to apply (use excludeName() if you don't have access to them). You can also exclude them via the spring.autoconfigure.exclude property. Auto-configuration is always applied after user-defined beans have been registered.

3. @ComponentScan - this enables component scan. It practically lets you declare other classes like @Component, @Service, @Controller and has Spring automatically discovere them AND REGISTER THEM AS BEANS IN THE SPRING CONTEXT.


## Spring boot

### Exclusions of auto configurations

Why would we want that? For optimization and better start time.

Exclusions are all or nothing and need to be used when you don't need configuration at all.

      spring.autoconfigure.exlclude = class1, class2 -> application.properties
      
      @EnableAutoConfiguration(exlude = {class1, class2})
      
Some of this autoconfigurations may depend on a property.Look into the spring boot documentation and see what properties are available for tuning.

You can also override @ConditionalOnMissingBean conditions and if you applications doesn't user Servlets of filters, the you can define a FilterRegistrationBean and call setEnabled(false);


