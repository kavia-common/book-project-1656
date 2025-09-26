# Backend Preview Setup (Spring Boot, Maven Wrapper)

This project uses Maven Wrapper and is a multi-module Spring Boot application. The main runnable module is `book-app`. For remote preview, ensure the backend binds to port `3001`.

## Working Directory
Use this directory as the working directory for all commands:
```
book-project-1656/backend
```

## Install (Build) Command
Non-interactive build skipping tests:
```
./mvnw -B -DskipTests=true clean package
```

## Start Command (Run via Maven)
Run the Spring Boot app from the `book-app` module:
```
./mvnw -B -DskipTests=true spring-boot:run -pl book-app -am
```

## Environment Variables
Force the app to bind to the preview port:
```
SERVER_PORT=3001
JAVA_TOOL_OPTIONS="-Dserver.port=3001"
SPRING_PROFILES_ACTIVE="default"
```

## Alternate Start (Run the built JAR)
After building, you can run the fat JAR:
```
java -Dserver.port=3001 -jar book-app/target/book-app-*.jar
```

## Health Check
If Spring Boot Actuator is enabled, a typical health endpoint is:
```
/actuator/health
```
The preview can use `http://localhost:3001/actuator/health` for readiness. If Actuator is not enabled, the preview should rely on the port open status instead.

## Notes
- The `-pl book-app -am` flags ensure the correct module is run and dependent modules are also built.
- `-B` makes Maven non-interactive for CI environments.
- Tests are skipped to speed up preview startup; remove `-DskipTests=true` for full verification.
