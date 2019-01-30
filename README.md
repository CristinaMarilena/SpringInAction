# SpringInAction

## SPRING ANNOTATIONS

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


## SPRING BOOT

### Exclusions of auto configurations

Why would we want that? For optimization and better start time.

Exclusions are all or nothing and need to be used when you don't need configuration at all.

      spring.autoconfigure.exlclude = class1, class2 -> application.properties
      
      @EnableAutoConfiguration(exlude = {class1, class2})
      
Some of this autoconfigurations may depend on a property.Look into the spring boot documentation and see what properties are available for tuning.

You can also override @ConditionalOnMissingBean conditions and if you applications doesn't user Servlets of filters, the you can define a FilterRegistrationBean and call setEnabled(false);

## INPUT VALIDATIONS

Spring supports java bean validation API wich makes it easy to declare validation rules as opposed to explicitly writing declaration login in your application.

**Apply validation rules with SPRING MVC:

1. Declare validation rules on the class that is validated(models)
2. Specify that the validation should be made in the controller s methods that require validation
3. Display validation errors

Ex: 

                  @NotNull
                  @Size(min, message)
                  @NotBlank    ( from hibernate)
                  @CreditCardNumber  
                  @Pattern 
                  @Digits
                  
**_Side note: - Pattern doesn t seem right to validate a date, but only the format of it. 
              - CreditCardNumber ann implements Luhn algorithm_**
              
To acutally validate the request data use the @Valid annotation to the corresponding model parameter.

## SPRING BOOT APPLICATION CONFIGURATION

Spring boot provides a very easy way for configuring your application regarding externalized properties. It lets you configure your application using a file named **_application.properties_**. 

### Application Configuration using @Value

            @RestController
            public class Welcome{
                  @Value ("${welcome.message}")
                  private String welcomeMessage;

                  //use the welcome message
            }

### Application Configuration using Type-safe Configuration Properties

The problem with @Value is that you have all you properties distributed through out you entire application. A better approach would be to have a centralized solution. You can define a configuration component using @ConfigurationProperties annotation 

            @Component
            @ConfigurationProperties("basic")
            public class BasicConfiguration {
                private boolean value;
                private String message;
                private int number;

                public boolean isValue() {
                    return value;
                }

                public void setValue(boolean value) {
                    this.value = value;
                }

                public String getMessage() {
                    return message;
                }

                public void setMessage(String message) {
                    this.message = message;
                }

                public int getNumber() {
                    return number;
                }

                public void setNumber(int number) {
                    this.number = number;
                }

            }

All the exposed properties of BasicConfiguration will now start with 'basic' : basic.value, basic.message etc;
Now you can autowire BasicConfiguration whenever you want to use it.

### Understand Type Safety

@ConfigurationProperties is type safe. That means that if you configure any property with an invalid type the application will fail to start.



