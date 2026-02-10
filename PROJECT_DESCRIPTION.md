# PlugNPlay — Project Overview

**Project:** A Spring Boot REST API for managing and sharing code snippets. Implements JWT authentication, OAuth2 social login, refresh tokens, role-based access, and basic CRUD for code snippets. Designed to run via Maven or inside Docker.

**Key Features:**
- JWT-based auth plus refresh tokens
- OAuth2 login support (multiple providers)
- User, Role, RefreshToken, CodeSnippet entities and repositories
- REST controllers for auth, users, snippets, and health checks
- Environment-specific properties (`application-*.properties`)
- Docker-ready via provided `Dockerfile`

**Build & Run (quick):**

- On Windows (wrapper present):

  ```powershell
  mvnw.cmd spring-boot:run
  ```

- On Unix/macOS:

  ```bash
  ./mvnw spring-boot:run
  ```

- Build jar and run:

  ```bash
  ./mvnw package
  java -jar target/*.jar
  ```

- Docker:

  ```bash
  docker build -t plugandplay .
  docker run -p 8080:8080 plugandplay
  ```

**Important files:**

- `pom.xml` — Maven project descriptor
- `Dockerfile` — container image build
- `mvnw`, `mvnw.cmd` — Maven wrapper for reproducible builds
- `src/main/resources/application*.properties` — environment configs

**High-level folder structure:**

```
./
├─ Dockerfile
├─ mvnw
├─ mvnw.cmd
├─ pom.xml
├─ src/
│  ├─ main/
│  │  ├─ java/
│  │  │  └─ com/PlugNPlay/www/
│  │  │     ├─ PlugNPlayApplication.java        # Spring Boot entrypoint
│  │  │     ├─ config/                          # APIDocConfig, CorsConfig, ProjectConfig
│  │  │     ├─ controller/                      # AuthController, UserController, SnippestController, HealthController
│  │  │     ├─ dto/                             # DTOs and responses
│  │  │     ├─ entity/                          # JPA entities: User, Role, CodeSnippest, RefreshToken, Code
│  │  │     ├─ enums/                           # Provider enum
│  │  │     ├─ exceptions/                      # GlobalExceptionsHandler, ResourceNotFoundException
│  │  │     ├─ repository/                      # Spring Data repositories for entities
│  │  │     ├─ security/                        # Security config, JWT filter, CustomUserDetailService
│  │  │     ├─ service/                         # Service interfaces and helpers (Auth, JWT, Cookie, OAuth handler)
│  │  │     └─ serviceImpl/                     # Service implementations
│  │  └─ resources/
│  │     ├─ application.properties
│  │     ├─ application-dev.properties
│  │     ├─ application-qa.properties
│  │     ├─ application-prod.properties
│  │     └─ static/                             # static assets
│  └─ test/
│     └─ java/...
└─ target/                                     # build output (ignored in VCS)
```

**What to look at first (dev onboarding):**

- `src/main/java/com/PlugNPlay/www/config/SecurityConfig.java` — how auth flows are wired
- `src/main/java/com/PlugNPlay/www/controller/AuthController.java` — endpoints for login/refresh
- `src/main/java/com/PlugNPlay/www/entity/CodeSnippest.java` and `repository/CodeSnippestRepository.java` — data model for snippets


---

