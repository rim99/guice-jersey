# Jersey Guice Module

## Introduction
Easy to use Google Guice module for Jersey.

##Installation

### Gradle

```goovy
compile 'io.logz:guice-jersey:1.0-SNAPSHOT'
```

### Maven

```xml
<dependency>
  <groupId>io.logz</groupId>
  <artifactId>guice-jersey</artifactId>
  <version>1.0-SNAPSHOT</version>
</dependency>
```
## Usage

### Getting Started

```java
public class Main {
    public static void main(String[] args) throws Exception {
        JerseyConfiguration configuration = JerseyConfiguration.builder()
            .addPackage("com.example.resources")
            .addPort(8080)
            .build();
        
        AtomicReference<Injector> injectorRef = new AtomicReference<>();
        
        List<Module> modules = new ArrayList<>();        
        modules.add(new JerseyModule(configuration, injectorRef::get));
        modules.add(new AbstractModule() {
          @Override
          protected void configure() {
            // Your module bindings ...
          }
        });
        
        Injector injector = Guice.createInjector(modules);
        injectorRef.set(injector);
        
        injector.getInstance(JerseyServer.class).start();
    }
}
```
