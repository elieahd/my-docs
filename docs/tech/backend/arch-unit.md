# ArchUnit with JUnit 5

[ArchUnit](https://www.archunit.org/) is a Java library that allows you to define and enforce architectural rules, such as package dependencies, naming conventions, and layer boundaries, using unit tests.

This helps maintain a clean architecture and prevents unwanted dependencies from creeping into your codebase. It also catch architectural violations early in the development process.

## Getting Started

### Add Dependency

```xml
<dependency>
  <groupId>com.tngtech.archunit</groupId>
  <artifactId>archunit-junit5</artifactId>
  <version>1.4.1</version>
  <scope>test</scope>
</dependency>
```

### Example of usage of Arch Unit

#### Ensuring your domain do not depends on external classes

This rule ensures that classes in your `domain` package only depend on other domain classes or JDK classes, enforcing a clean domain model.

```java
@AnalyzeClasses(
    packages = "com.socgen.mycontrols",
    importOptions = DoNotIncludeTests.class
)
class DomainArchTest {

    @ArchTest
    static final ArchRule domainShouldNotDependOnExternalClasses = classes()
        .that().resideInAPackage("..domain..")
        .should().onlyDependOnClassesThat().resideInAPackage(
            "com.socgen.mycontrols.domain..",
            "java.."
        );
}
```

#### Ensuring a package only contains interfaces

This rule enforces that all classes in the `domain.inbound` package are interfaces, which is useful for defining ports in a hexagonal architecture.

```java
@AnalyzeClasses(
    packages = "com.socgen.mycontrols",
    importOptions = DoNotIncludeTests.class
)
class DomainArchTest {

    @ArchTest
    static final ArchRule inboundShouldOnlyBeInterfaces = classes()
        .that().resideInAPackage("..domain.inbound..")
        .should().beInterfaces();
}
```

#### Ensuring all classes are annotated under a package and have a name

This rule checks that all classes in the `domain.usecases` package are annotated with `@UseCase` and their names end with `UseCase`.

```java
@AnalyzeClasses(
    packages = "com.socgen.mycontrols",
    importOptions = DoNotIncludeTests.class
)
class DomainArchTest {

    @ArchTest
    static final ArchRule useCasesShouldBeAnnotatedAndShouldHaveUseCaseAtTheEndAsName = classes()
        .that().resideInAPackage("..domain.usecases..")
        .should().beAnnotatedWith(UseCase.class)
        .andShould().haveSimpleNameEndingWith("UseCase");
}
```

## Resources

- [ArchUnit Official Documentation](https://www.archunit.org/userguide/html/000_Index.html)
- [ArchUnit Examples on GitHub](https://github.com/TNG/ArchUnit-Examples)
