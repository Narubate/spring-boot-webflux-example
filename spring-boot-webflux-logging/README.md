# spring-boot-webflux-logging
ตัวอย่างการเขียน Spring-boot WebFlux Logging 

# 1. เพิ่ม Dependencies

pom.xml 
``` xml
...
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.5.RELEASE</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-webflux</artifactId>
    </dependency>
    
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <scope>provided</scope>
    </dependency>
</dependencies>

...
```

lombox เป็น dependency ที่ใช้สำหรับ generate code จาก annotation ต่าง ๆ   
เอกสาร [https://projectlombok.org/](https://projectlombok.org/)  

# 2. เขียน Main Class 

``` java
@SpringBootApplication
@ComponentScan(basePackages = {"com.pamarin"}) 
public class AppStarter {

    public static void main(String[] args) {
        SpringApplication.run(AppStarter.class, args);
    }

}
```

# 3. เขียน Controller
``` java
@Slf4j
@RestController
public class HomeController {

    @GetMapping({"", "/"})
    public Mono<String> hello() {
        log.debug("call hello method");
        return Mono.just("Hello world.");
    }
}
```

@Slf4j เป็นการใช้ annotation ของ lombox เพื่อ generate Log4J Code (logging)  
ทำให้เราไม่ต้องเขียน new instance ของ log4j เอง  
การทำงานของ lombox เป็นการ inject code at compile time  

# 4. Config Logging
classpath:application.properties 
``` properties 
logging.level.org.springframework=DEBUG
logging.level.com.pamarin=DEBUG
logging.file=/log/app.log
```
# 5. Build
cd ไปที่ root ของ project จากนั้น  
``` shell 
$ mvn clean install
```

# 6. Run 
``` shell 
$ mvn spring-boot:run
```

# 7. เข้าใช้งาน

เปิด browser แล้วเข้า [http://localhost:8080](http://localhost:8080)


# เอกสารเพิ่มเติม 
- [https://docs.spring.io/spring-boot/docs/current/reference/html/howto-logging.html](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-logging.html)  
