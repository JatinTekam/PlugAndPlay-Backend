# PlugNPlay

Lightweight Spring Boot service for managing and sharing code snippets. See PROJECT_DESCRIPTION.md for a high-level overview.

**Quick start**

Prerequisites: JDK + Maven wrapper (provided).

On Windows:

    mvnw.cmd spring-boot:run

On Unix/macOS:

    ./mvnw spring-boot:run

Build jar:

    ./mvnw package
    java -jar target/*.jar

Docker:

    docker build -t plugandplay .
    docker run -p 8080:8080 plugandplay

Configuration: environment-specific properties are in `src/main/resources`:

- `application.properties`, `application-dev.properties`, `application-qa.properties`, `application-prod.properties`.

Key files:

- `pom.xml` — Maven config
- `Dockerfile` — container image build
- `src/main/java/com/PlugNPlay/www/config/SecurityConfig.java` — security wiring
- `src/main/java/com/PlugNPlay/www/controller/AuthController.java` — auth endpoints
- `src/main/java/com/PlugNPlay/www/controller/SnippestController.java` — snippet endpoints

Example API usage (adjust base path and endpoints to match controllers in code):

- Health check

    curl http://localhost:8080/actuator/health

- Register (example) — adjust endpoint and payload as implemented in `AuthController`

    curl -X POST http://localhost:8080/api/auth/register \
      -H "Content-Type: application/json" \
      -d '{"username":"alice","email":"alice@example.com","password":"Secret123"}'

- Login (returns JWT + refresh token)

    curl -X POST http://localhost:8080/api/auth/login \
      -H "Content-Type: application/json" \
      -d '{"usernameOrEmail":"alice","password":"Secret123"}'

- Refresh token

    curl -X POST http://localhost:8080/api/auth/refresh \
      -H "Content-Type: application/json" \
      -d '{"refreshToken":"<token-here>"}'

- Create a snippet (authenticated)

    curl -X POST http://localhost:8080/api/snippets \
      -H "Content-Type: application/json" \
      -H "Authorization: Bearer <JWT>" \
      -d '{"title":"Example","code":"console.log(\"hi\")","language":"javascript"}'

- List snippets (public or authenticated depending on implementation)

    curl http://localhost:8080/api/snippets

Notes:

- Verify the exact endpoint paths and request/response formats in `src/main/java/com/PlugNPlay/www/controller/`.

See also: PROJECT_DESCRIPTION.md for the detailed folder tree and suggestions.
