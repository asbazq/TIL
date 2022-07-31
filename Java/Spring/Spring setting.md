# Spring 기본설정

1. spring web
2. MySQL Driver
3. H2 Database
4. Spring Data JPA
5. Lombok
6. Spring securuty
7. spring boot DevTool
8. Mustache

        dependencies {
          implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
          implementation 'org.springframework.boot:spring-boot-starter-mustache'
          implementation 'org.springframework.boot:spring-boot-starter-security'
          implementation 'org.springframework.boot:spring-boot-starter-web'
          compileOnly 'org.projectlombok:lombok'
          developmentOnly 'org.springframework.boot:spring-boot-devtools'
          runtimeOnly 'com.h2database:h2'
          runtimeOnly 'mysql:mysql-connector-java'
          annotationProcessor 'org.projectlombok:lombok'
          testImplementation 'org.springframework.boot:spring-boot-starter-test'
          testImplementation 'org.springframework.security:spring-security-test'
