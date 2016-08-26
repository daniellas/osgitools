# OSGI Tools

This library provides @ImportPackages annotation than can be used as marker for tools like **Maven Bundle Plugin** to generate proper **Import-Package** entries in manifest file. 

Import-Package manifest entry is required in OSGI environment, so if you don't use OSGI, don't bother.

## Usage

Just annotate any class in your project like this:

```java
@ImportPackages({MyClass.class})
public class PackageImports {
}
```
