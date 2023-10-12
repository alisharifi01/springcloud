# springcloud


<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-stream-azure</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-stream</artifactId>
    </dependency>
</dependencies>


import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.stream.function.StreamBridge;
import org.springframework.context.annotation.Bean;
import java.util.function.Consumer;

@SpringBootApplication
public class ServiceBusProducerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ServiceBusProducerApplication.class, args);
    }

    @Bean
    public Consumer<String> messageSender(StreamBridge streamBridge) {
        return message -> {
            streamBridge.send("output", message);
            System.out.println("Sent message: " + message);
        };
    }
}



spring.cloud.stream.bindings.output.destination=your-queue-name
spring.cloud.azure.servicebus.connection-string=your-connection-string




