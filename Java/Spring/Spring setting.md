# Spring 기본설정

1. spring web
2. MySQL Driver
3. H2 Database
4. Spring Data JPA
5. Lombok
6. Spring security
7. spring boot DevTool
8. Mustache

build.gradle

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

application.yml

        server:
          port: 8080
          servlet:
            context-path: /
            encoding:
              charset: UTF-8
              enabled: true
              force: true

        spring:
          datasource:
            driver-class-name: com.mysql.cj.jdbc.Driver
            url: jdbc:mysql://localhost:3306/security?serverTimezone=Asia/Seoul
            username: cos
            password: cos1234

          mvc:
            view:
              prefix: /templates/
              suffix: .mustache

          jpa:
            hibernate:
              ddl-auto: update #create update none
              naming:
                physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
            show-sql: true
