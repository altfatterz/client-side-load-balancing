## Setup 

1. Clone the project

```bash
$ git clone http://github.com/altfatter/client-side-load-balancing
$ cd client-side-load-balancing/ribbon
```

2. Start the `say-hello-service` application 

```bash
$ java -jar say-hello-service/target/say-hello-service-0.0.1-SNAPSHOT.jar
```

3. Start the `say-hello-client` application

```bash
$ java -jar say-hello-service/target/say-hello-client-0.0.1-SNAPSHOT.jar
```

4. Make a request:

```bash
zoal@Zoltans-MacBook-Pro:~|⇒  http :8080/hi\?name=Zoltan
HTTP/1.1 200
Content-Length: 20
Content-Type: text/plain;charset=UTF-8
Date: Wed, 09 May 2018 15:04:57 GMT

Salutations, Zoltan!
```
 
5. Start more instances of the `say-hello-service` application

```bash
$ java -jar say-hello-service/target/say-hello-service-0.0.1-SNAPSHOT.jar --server.port=8082
$ java -jar say-hello-service/target/say-hello-service-0.0.1-SNAPSHOT.jar --server.port=8083
```

6. Verify that the `http :8080/hi` request is load balanced across the `say-hello-service` instances. 