- [Spring Cloud Gateway](#spring-cloud-gateway)
	- [설정 방법](#설정-방법)
	- [References](#references)

# Spring Cloud Gateway

- Built on Spring Framework 5, Project Reactor and Spring Boot 2.0

- Able to match routes on any request attribute.

- Predicates and filters are specific to routes.

- Circuit Breaker integration.

- Spring Cloud DiscoveryClient integration

- Easy to write Predicates and Filters

- Request Rate Limiting

- Path Rewriting

## 설정 방법

`application.yml`

```yaml
spring:
  cloud:
    gateway:
      routes:
			# routing block 단위
      - id: after_route
        uri: https://example.org
        predicates:
        - Cookie=mycookie,mycookievalue
```

`java`

```Java
@Bean
public RouteLocator routes(RouteLocatorBuilder builder) {
    return builder.routes()
        .route("rewrite_response_upper", r -> r.host("*.rewriteresponseupper.org")
            .filters(f -> f.prefixPath("/httpbin")
                .modifyResponseBody(String.class, String.class,
                    (exchange, s) -> Mono.just(s.toUpperCase()))).uri(uri)
        .build();
}
```

## References

- https://spring.io/projects/spring-cloud-gateway