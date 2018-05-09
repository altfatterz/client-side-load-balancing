## Setup 

1. Clone the project

```bash
$ git clone http://github.com/altfatter/client-side-load-balancing
$ cd client-side-load-balancing/eureka
```

2. Start Eureka Server

```
$ java -jar eureka-server/target/eureka-server-0.0.1-SNAPSHOT.jar
```

3. Verify that the `Eureka Dashboard` is available at `http://localhost:8761`


4. Start the `say-hello-service` application 

```bash
$ java -jar say-hello-service/target/say-hello-service-0.0.1-SNAPSHOT.jar
```

In the logs you should see that registered with `Eureka Server`:

```bash
2018-05-09 15:31:49.437  INFO 15973 --- [nfoReplicator-0] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_SAY-HELLO-SERVICE/192.168.87.65:say-hello-service:8081 - registration status: 204
```

Verify also on the Eureka Dashboard that once instance of the `say-hello-service` is registered with `Eureka Server` 

5. Start the `say-hello-client` application

```bash
$ java -jar say-hello-service/target/say-hello-client-0.0.1-SNAPSHOT.jar
```

In the logs you should see

```bash
2018-05-09 17:03:58.916  INFO 18875 --- [nfoReplicator-0] com.netflix.discovery.DiscoveryClient    : DiscoveryClient_SAY-HELLO-CLIENT/192.168.87.65:say-hello-client - registration status: 204
```

Verify also on the Eureka Dashboard that by now both the `say-hello-service` and `say-hello-client` is registered with `Eureka Server`

6. Make a request:

```bash
zoal@Zoltans-MacBook-Pro:~|⇒  http :8080/hi\?name=Zoltan
HTTP/1.1 200
Content-Length: 20
Content-Type: text/plain;charset=UTF-8
Date: Wed, 09 May 2018 15:04:57 GMT

Salutations, Zoltan!
```

If you kill the Eureka Server it still works since the `say-hello-client` caches the address of the `say-hello-service`.
 
