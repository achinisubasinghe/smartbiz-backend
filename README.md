# SmartBiz Backend

SmartBiz Backend is a REST API for multi-business inventory, sales, invoicing, expense, and subscription management, built with Spring Boot 3.5, Spring Security, JWT authentication, and MariaDB.

## Features

- **JWT authentication and password reset.** User registration, sign-in, token validation through `JwtAuthenticationFilter`, and SMTP password reset emails with expiring tokens stored in `ChangePasswordTokenRepo`.
- **Business and subscription management.** CRUD endpoints for business owners, businesses, and subscription plans.
- **Catalog and stock tracking.** Manage products by SKU, query low-stock items at `/api/products/low-stock`, and track supplier inventory records per business.
- **Orders, sales, and invoicing.** Record customer orders, link sales to orders and inventory items, and generate invoices per sale.
- **Income and expense ledger.** Track business income entries and categorized expenses defined by `ExpenseType`.

## Tech stack

- Java 17 and [Spring Boot](https://spring.io/projects/spring-boot) 3.5.6
- Spring Web, Spring Data JPA, Spring Security, Spring Validation, and Spring Mail
- [MariaDB](https://mariadb.org) JDBC driver and Hibernate ORM
- JSON Web Tokens via `jjwt` 0.11.5
- Lombok and Maven

## API endpoints

| Base path | Operations |
| --- | --- |
| `/signUp`, `/signIn`, `/logout`, `/send-reset-email`, `/reset-password-confirm` | Account registration, JWT login, logout, and email password reset |
| `/api/users` | List, fetch by ID, search, and delete user accounts |
| `/api/owners` | Create, list, fetch by ID or name, update, and delete business owners |
| `/api/businesses` | Create, list, fetch by ID or name, update, and delete businesses |
| `/api/subscription-plans` | Create, list, fetch by ID or name, update, and delete subscription plans |
| `/api/customers` | Create, list, fetch by ID, name, or business, update, and delete customers |
| `/api/suppliers` | Create, list, fetch by ID, name, or business, update, and delete suppliers |
| `/api/products` | Create, list, fetch by ID or SKU, query `/low-stock`, update, and delete products |
| `/api/inventories` | Create, list, fetch by ID, business, or supplier, update, and delete inventory rows |
| `/api/orders` | Create, list, fetch by ID, customer, or business, update, and delete orders |
| `/api/sales` | Create, list, fetch by ID, order, or inventory, update, and delete sales |
| `/api/invoices` | Create, list, fetch by ID or sale, update, and delete invoices |
| `/api/incomes` | Create, list, fetch by ID or business, update, and delete income records |
| `/api/expenses` | Create, list, fetch by ID or business, update, and delete expense records |

## Getting started

### Prerequisites

- Java 17 SDK
- MariaDB server running on port `3306`
- SMTP credentials such as Mailtrap for password reset emails

### Configuration

Edit `src/main/resources/application.properties`:

```properties
server.port=8080
spring.datasource.url=jdbc:mariadb://localhost:3306/smartbiz
spring.datasource.username=your_db_user
spring.datasource.password=your_db_password

jwt.secret=your_base64_jwt_secret
jwt.expiration-ms=86400000
spring.jpa.hibernate.ddl-auto=update

spring.mail.host=sandbox.smtp.mailtrap.io
spring.mail.port=587
spring.mail.username=your_smtp_user
spring.mail.password=your_smtp_password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

### Build and run

```bash
git clone https://github.com/achinisubasinghe/smartbiz-backend.git
cd smartbiz-backend
./mvnw spring-boot:run
```

The server listens on `http://localhost:8080`.

Run the test suite or build an executable JAR:

```bash
./mvnw test
./mvnw clean package
```

## Project structure

```text
smartbiz-backend/
├── src/
│   ├── main/
│   │   ├── java/com/smartbiz/
│   │   │   ├── config/
│   │   │   ├── controller/
│   │   │   ├── dto/
│   │   │   │   ├── request/
│   │   │   │   └── response/
│   │   │   ├── entity/
│   │   │   ├── enums/
│   │   │   ├── exception/
│   │   │   ├── repo/
│   │   │   ├── service/
│   │   │   │   └── impl/
│   │   │   ├── util/
│   │   │   └── SmartBizApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
├── mvnw
└── pom.xml
```
