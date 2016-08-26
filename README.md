# OSGI Tools

This library provides **@ImportPackages** annotation than can be used as marker for tools like **Maven Bundle Plugin** to generate proper **Import-Package** entries in manifest file. 

Import-Package manifest entry is required in OSGI environment, so if you don't use OSGI, don't bother.

## Usage

Just annotate any class in your project like this:

```java
@ImportPackages({MyClass.class,AnyOtherClass.class})
public class PackageImports {
}
```

and configure Maven Bundle Plugin in you project pom.xml like this:

```xml
<plugin>
    <groupId>org.apache.felix</groupId>
    <artifactId>maven-bundle-plugin</artifactId>
    <version>2.5.3</version>
    <configuration>
        <instructions>
            <Import-Package>
                !com.lynx.osgitools,
                *
            </Import-Package>
        </instructions>
    </configuration>
</plugin>
```

Above configuration will cause:

* Maven Bundle Plugin will add appropriate packages for all classes used in your project. * (asterisk) in `<Import-Package>` is responsible for that
* Since you added classes to `@ImportPackages` value, their packages will be added to your manifest

## Why?

I used it personally because other options are:

1. Add proper packages inside `<Import-Package>` in pom.xml manually
2. Create dummy fields in some class like `private MyClass myClass;`

None of the above options satisfies me ;)

## Installation in OSGI container

Osgitools it OSGI bundle itself, so you can install it in your container and omit **!com.lynx.osgitools** 

In that case your Maven Bundle Plugin configuration can be stripped to:

```xml
<plugin>
    <groupId>org.apache.felix</groupId>
    <artifactId>maven-bundle-plugin</artifactId>
    <version>2.5.3</version>
    <configuration>
        <instructions>
            <Import-Package>
                *
            </Import-Package>
        </instructions>
    </configuration>
</plugin>
```
## Installation

Latest rrelease version is **1.0.2**

1. git clone git@github.com:daniellas/osgitools.git
2. git checkout tags/osgitools-1.0.2
3. mvn clean install