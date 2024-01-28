# junit 5 모듈 구성

### Build.gradle 설정
```groovy
plugins {
    id 'java'
    id 'eclipse'
    id 'idea'
}


sourceCompatibility = '1.8'
targetCompatibility = '1.8'
compileJava.options.encoding = 'UTF-8'
compileTestJava.options.encoding = 'UTF-8'

repositories {
    mavenCentral()
}

dependencies {
    testImplementation('org.junit.jupiter:junit-jupiter:5.5.0')
}

test {
    useJUnitPlatform()
    testLogging {
        events "passed", "skipped", "failed"
    }
}
```

### Spring Boot에서 Junit5 이용하기
- `spring-boot-starter-test:3.2.2` 기준, 하위 dependency에 junit.jupiter v5를 포함
    ![img.png](img.png)
- spring boot 2.4 버전부터 junit vintage engine이 제거 되었기 때문에 명시적으로 dependency 추가 필요
  - JUnit 5’s Vintage Engine Removed from spring-boot-starter-test
    If you upgrade to Spring Boot 2.4 and see test compilation errors for JUnit classes such as org.junit.Test, this may be because JUnit 5’s vintage engine has been removed from spring-boot-starter-test. The vintage engine allows tests written with JUnit 4 to be run by JUnit 5. If you do not want to migrate your tests to JUnit 5 and wish to continue using JUnit 4, add a dependency on the Vintage Engine, as shown in the following example for Maven


### `useJunitPlatform()`설정은 꼭 추가해야하는가?

- 요약
  - Gradle 5.x 버전 이상은 junit-jupiter dependency가 포함될 경우 test 실행에 사용함
  - Junit과 Gradle 통합 구성이 되어있으므로 이 설정을 추가하지 않도라도 junit 5를 사용하도록 구성됨
  - 해당 설정을 꼭 사용할 필요는 없지만 모듈에서 명시적으로 junit 5를 사용한다는 것을 알려줄 수 있으므로 사용하는 것을 권장 

> By ChatGPT
> 
If you have a JUnit 5 dependency in your build.gradle file but don't use useJUnitPlatform(), Gradle will still recognize and use the JUnit 5 engine for running tests by default. This behavior is a result of the integration between Gradle and the JUnit Platform.

The JUnit Platform is designed to provide a unified platform for executing tests, and it supports both JUnit 4 and JUnit 5 tests. When you include a JUnit 5 dependency in your build file, Gradle automatically configures itself to use the JUnit Platform for test execution.

Here's an example of a build.gradle file with a JUnit 5 dependency:

```groovy
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.7.2'
}
```
In this case, you don't explicitly need to use useJUnitPlatform() in your Gradle configuration. The presence of the JUnit 5 dependency in the classpath signals to Gradle that it should use the JUnit Platform for running tests.

If you want to be explicit or if you have a more complex setup, you can include useJUnitPlatform() in your test configuration:

```groovy
test {
    useJUnitPlatform()
}
```
Including this configuration explicitly ensures that Gradle uses the JUnit Platform for running tests. However, in many cases, it's not strictly necessary, as Gradle will automatically detect and use the JUnit Platform when it finds JUnit 5 dependencies in the classpath.






