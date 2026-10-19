# Product Management API - Spring Boot REST API

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.7-brightgreen)
![Java](https://img.shields.io/badge/Java-21-orange)
![H2 Database](https://img.shields.io/badge/H2-In--Memory-blue)

A complete RESTful API for product management using Spring Boot, Spring Data JPA, H2 Database, and Swagger/OpenAPI documentation.

## 📋 Table of Contents

- [Features](#features)
- [Technologies](#technologies)
- [Requirements](#requirements)
- [Installation and Running](#installation-and-running)
- [API Endpoints](#api-endpoints)
- [Request Examples](#request-examples)
- [Swagger UI](#swagger-ui)
- [H2 Console](#h2-console)
- [Project Structure](#project-structure)
- [Error Handling](#error-handling)

## 🚀 Features

- ✅ CRUD operations for product management
- ✅ REST API with JSON format
- ✅ H2 Database integration (in-memory)
- ✅ Swagger/OpenAPI documentation
- ✅ Global exception handling
- ✅ Spring Data JPA for database operations
- ✅ Data validation
- ✅ H2 Web Console for data viewing

## 🛠 Technologies

- **Java 21**
- **Spring Boot 3.5.7**
  - Spring Web
  - Spring Data JPA
  - Spring Boot DevTools
- **H2 Database** (in-memory)
- **Springdoc OpenAPI 2.7.0** (Swagger UI)
- **Gradle** (build tool)

## 📦 Requirements

- Java Development Kit (JDK) 21 or higher
- Gradle (wrapper included in the project)
- IDE (IntelliJ IDEA recommended)

## 🔧 Installation and Running

### Method 1: Via IntelliJ IDEA

1. Open the project in IntelliJ IDEA
2. Wait for Gradle to download all dependencies
3. Click the **"Reload All Gradle Projects"** button in the Gradle panel (right side)
4. Find the `SecondProjectApplication.java` class
5. Click the green ▶️ **Run** button next to the `main()` method

### Method 2: Via Command Line (Windows)

```cmd
# Build the project
.\gradlew.bat clean build

# Run the application
.\gradlew.bat bootRun
```

### Method 3: Run JAR file

```cmd
# Build JAR
.\gradlew.bat build

# Run
java -jar build\libs\second-project-0.0.1-SNAPSHOT.jar
```

After successful startup, the application will be available at: **http://localhost:8080**

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v1/products` | Get all products |
| `GET` | `/api/v1/products/{id}` | Get product by ID |
| `POST` | `/api/v1/products` | Create a new product |
| `PUT` | `/api/v1/products/{id}` | Update a product |
| `DELETE` | `/api/v1/products/{id}` | Delete a product |

## 💡 Request Examples

### 1. Create a new product (POST)

```bash
curl -X POST http://localhost:8080/api/v1/products \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Coffee\",\"description\":\"Arabica Beans\",\"price\":9.99}"
```

**Response (201 Created):**
```json
{
  "id": 1,
  "name": "Coffee",
  "description": "Arabica Beans",
  "price": 9.99
}
```

### 2. Get all products (GET)

```bash
curl http://localhost:8080/api/v1/products
```

**Response (200 OK):**
```json
[
  {
    "id": 1,
    "name": "Coffee",
    "description": "Arabica Beans",
    "price": 9.99
  },
  {
    "id": 2,
    "name": "Tea",
    "description": "Green Tea",
    "price": 5.50
  }
]
```

### 3. Get product by ID (GET)

```bash
curl http://localhost:8080/api/v1/products/1
```

**Response (200 OK):**
```json
{
  "id": 1,
  "name": "Coffee",
  "description": "Arabica Beans",
  "price": 9.99
}
```

### 4. Update product (PUT)

```bash
curl -X PUT http://localhost:8080/api/v1/products/1 \
  -H "Content-Type: application/json" \
  -d "{\"name\":\"Coffee Premium\",\"description\":\"Premium Arabica Beans\",\"price\":12.99}"
```

**Response (200 OK):**
```json
{
  "id": 1,
  "name": "Coffee Premium",
  "description": "Premium Arabica Beans",
  "price": 12.99
}
```

### 5. Delete product (DELETE)

```bash
curl -X DELETE http://localhost:8080/api/v1/products/1
```

**Response (204 No Content)**

### 6. Error - Product not found

```bash
curl http://localhost:8080/api/v1/products/999
```

**Response (404 Not Found):**
```json
{
  "timestamp": "2025-11-05T00:00:00.000000000Z",
  "message": "Product not found with id: 999"
}
```

## 📚 Swagger UI

Swagger UI provides interactive API documentation where you can test all endpoints directly in the browser.

**URL:** http://localhost:8080/swagger-ui/index.html

### Swagger UI Features:
- 📖 Complete documentation of all endpoints
- 🧪 Interactive API testing
- 📝 Request and response schemas
- ✅ Sample data

### OpenAPI JSON:
**URL:** http://localhost:8080/v3/api-docs

## 🗄️ H2 Console

H2 Console allows you to view and manage database data through a web interface.

**URL:** http://localhost:8080/console

### Connection Settings:
- **JDBC URL:** `jdbc:h2:mem:testdb`
- **Driver Class:** `org.h2.Driver`
- **Username:** `sa`
- **Password:** _(leave empty)_

### SQL queries for testing:

```sql
-- View all products
SELECT * FROM product;

-- Create product
INSERT INTO product (name, description, price) VALUES ('Laptop', 'Gaming Laptop', 1299.99);

-- Update product
UPDATE product SET price = 1199.99 WHERE id = 1;

-- Delete product
DELETE FROM product WHERE id = 1;
```

## 📁 Project Structure

```
second-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── dev/coffeedev/second_project/
│   │   │       ├── SecondProjectApplication.java          # Main class
│   │   │       ├── product/
│   │   │       │   ├── api/
│   │   │       │   │   ├── ProductController.java         # REST Controller
│   │   │       │   │   ├── request/
│   │   │       │   │   │   └── ProductRequest.java        # Request DTO
│   │   │       │   │   └── response/
│   │   │       │   │       └── ProductResponse.java       # Response DTO
│   │   │       │   ├── domain/
│   │   │       │   │   └── Product.java                   # JPA Entity
│   │   │       │   ├── repository/
│   │   │       │   │   └── ProductRepository.java         # JPA Repository
│   │   │       │   ├── service/
│   │   │       │   │   └── ProductService.java            # Business logic
│   │   │       │   └── support/
│   │   │       │       └── ProductMapper.java             # DTO mapper
│   │   │       ├── support/
│   │   │       │   └── exception/
│   │   │       │       ├── ProductNotFoundException.java  # Custom exception
│   │   │       │       ├── ProductExceptionSupplier.java  # Exception factory
│   │   │       │       └── GlobalExceptionHandler.java    # @ControllerAdvice
│   │   │       └── shared/
│   │   │           └── api/
│   │   │               └── response/
│   │   │                   └── ErrorMessageResponse.java  # Error DTO
│   │   └── resources/
│   │       ├── application.properties                     # Configuration
│   │       ├── static/                                    # Static files
│   │       └── templates/                                 # Templates
│   └── test/
│       └── java/
│           └── dev/coffeedev/second_project/
│               └── SecondProjectApplicationTests.java     # Tests
├── build.gradle                                           # Gradle config
├── settings.gradle
├── gradlew                                                # Gradle wrapper (Unix)
├── gradlew.bat                                            # Gradle wrapper (Windows)
├── .gitignore
└── README.md
```

## 🎯 Layer Architecture

```
Controller Layer (ProductController)
    ↓ receives HTTP requests, returns ResponseEntity
Service Layer (ProductService)
    ↓ business logic
Repository Layer (ProductRepository)
    ↓ JPA operations
Database (H2)
```

## ⚠️ Error Handling

The application uses a global exception handler (`@ControllerAdvice`) for unified error responses.

### Error Response Examples:

**404 Not Found:**
```json
{
  "timestamp": "2025-11-05T00:00:00.000000000Z",
  "message": "Product not found with id: 999"
}
```

**500 Internal Server Error:**
```json
{
  "timestamp": "2025-11-05T00:00:00.000000000Z",
  "message": "Internal server error occurred"
}
```

## 🧪 Testing

### Run tests:

```cmd
.\gradlew.bat test
```

### Test Report:
After running tests, the report is available at:
```
build/reports/tests/test/index.html
```

## 📝 Configuration (application.properties)

```properties
# Application name
spring.application.name=second-project

# H2 Database Configuration
spring.h2.console.enabled=true
spring.h2.console.path=/console
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver

# JPA Configuration
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=update
```

## 🔍 Useful Commands

```cmd
# View dependencies
.\gradlew.bat dependencies

# Clean build directory
.\gradlew.bat clean

# Build without tests
.\gradlew.bat build -x test

# Stop Gradle daemon
.\gradlew.bat --stop

# Run with profile
.\gradlew.bat bootRun --args='--spring.profiles.active=dev'
```

## Img
Get
![create](/doc/1.png)
Create
![create](/doc/2.png)
Get list
![create](/doc/3.png)
Delete
![create](/doc/4.png)
Update
![create](/doc/5.png)
## 📄 License

This project was created for educational purposes.

---

**Project Status:** ✅ Ready to use

**Created:** November 2025
