# api-spring-boot-gradle

0. To build [COMPILE+TEST+JAR]
    ./gradlew build


1. To run application
    gradle bootRun
OR after  build
    java -jar build/libs/api-spring-boot-gradle-0.1.0.jar

2. To test api
    http://localhost:8080/greeting

3. To build all
    ./gradlew clean build jacocoTestReport sonarqube  -Dsonar.host.url=http://azu-jenkins01:9000 -Dsonar.login=***** -Dsonar.password=*****
    OR
    gradle clean build jacocoTestReport sonarqube  -Dsonar.host.url=http://azu-jenkins01:9000 -Dsonar.login=***** -Dsonar.password=*****
