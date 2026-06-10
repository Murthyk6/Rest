# 🔌 REST API Practice — Spring Boot

> A focused REST API project built to master production-grade API design patterns in Spring Boot — covering resource modeling, HTTP semantics, error handling, and persistence. Serves as a reference implementation for RESTful service design used in backend and DevOps work.

![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.x-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![REST](https://img.shields.io/badge/REST-API-0052CC?style=flat-square)
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-Hibernate-59666C?style=flat-square)

---

## Purpose

This repo captures REST API patterns practiced as part of backend engineering training at MountBlue Technologies — the same skills applied when building the SIP Usage Portal backend at Ubona Technologies (Spring Boot + reactive REST APIs for telecom data aggregation).

---

## Concepts Covered

### HTTP & REST Fundamentals

| Pattern | Implementation |
|---|---|
| Resource naming | Noun-based, plural endpoints (`/posts`, `/users`) |
| HTTP methods | `GET`, `POST`, `PUT`, `PATCH`, `DELETE` semantics |
| Status codes | `200`, `201`, `204`, `400`, `404`, `409`, `500` |
| Request/Response | `@RequestBody`, `@ResponseBody`, DTOs |
| Path variables | `@PathVariable`, `@RequestParam` |

### Spring Boot Patterns

```java
@RestController
@RequestMapping("/api/v1/posts")
public class PostController {

    @GetMapping("/{id}")
    public ResponseEntity<PostDto> getById(@PathVariable Long id) { ... }

    @PostMapping
    public ResponseEntity<PostDto> create(@Valid @RequestBody PostRequest req) { ... }

    @PutMapping("/{id}")
    public ResponseEntity<PostDto> update(@PathVariable Long id, @RequestBody PostRequest req) { ... }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(@PathVariable Long id) { ... }
}
```

### Error Handling

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(404).body(new ErrorResponse(ex.getMessage()));
    }
}
```

---

## Running Locally

```bash
git clone https://github.com/Murthyk6/Rest.git
cd Rest
./mvnw spring-boot:run
```

Test endpoints:

```bash
# Get all resources
curl -X GET http://localhost:8080/api/v1/posts

# Create a resource
curl -X POST http://localhost:8080/api/v1/posts \
  -H "Content-Type: application/json" \
  -d '{"title": "My Post", "content": "Hello World"}'

# Update
curl -X PUT http://localhost:8080/api/v1/posts/1 \
  -H "Content-Type: application/json" \
  -d '{"title": "Updated"}'

# Delete
curl -X DELETE http://localhost:8080/api/v1/posts/1
```

---

## Skills This Demonstrates

- Backend API design for DevOps tooling and internal dashboards
- REST fundamentals underpinning the SIP Usage Portal (Mono/Flux reactive APIs)
- Spring Boot proficiency used in production at MountBlue and Ubona Technologies

---

> Part of a progression: REST basics → Spring Boot production services → reactive APIs (used in telecom analytics platform at Ubona Technologies).
