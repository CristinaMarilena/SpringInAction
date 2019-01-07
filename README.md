# SpringInAction

## Spring annotations

### @Component
This simple annotation identifies the class as a component class and serves as a clue to Spring that a bean should be created for the class.

### @ComponentScan
Enables spring scan in the package and all the subpackeges, looking for classes annotated with @Component.

## Spring boot

### Exclusions of auto configurations

Why would we want that? For optimization and better start time.

Exclusions are all or nothing and need to be used when you don't need configuration at all.

      spring.autoconfigure.exlclude = class1, class2 -> application.properties
      
      @EnableAutoConfiguration(exlude = {class1, class2})
      
Some of this autoconfigurations may depend on a property.Look into the spring boot documentation and see what properties are available for tuning.

You can also override @ConditionalOnMissingBean conditions and if you applications doesn't user Servlets of filters, the you can define a FilterRegistrationBean and call setEnabled(false);


