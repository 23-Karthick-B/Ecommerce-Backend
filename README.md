# Ecommerce Backend API (Spring Boot)

## Project Overview
This project is a **Spring Boot based E-commerce backend API** that provides REST endpoints for managing:

- Product catalog
- Product search and filtering
- Product reviews
- Order creation and retrieval

The application is built using **Spring Boot, Spring Data JPA, and REST APIs** and demonstrates a modular backend architecture for an e-commerce system.

---

# Tech Stack

| Technology | Purpose |
|---|---|
| Java | Programming Language |
| Spring Boot | Backend Framework |
| Spring Data JPA | Database ORM |
| Hibernate | Persistence |
| Maven | Dependency Management |
| REST API | Client-server communication |

---

# Project Architecture

The project follows a **layered architecture**.

```
Controller Layer
       ↓
Service Layer
       ↓
Repository Layer
       ↓
Database
```

### Controller
Handles HTTP requests and exposes REST APIs.

### Service
Contains business logic and processing.

### Repository
Handles database operations using Spring Data JPA.

### Entity
Represents database tables.

---

# Project Structure

```
src/main/java/com/project/ecommerce

├── controller
│   ├── ProductController.java
│   ├── ProductReviewController.java
│   └── OrderController.java
│
├── service
│   ├── ProductService.java
│   └── OrderService.java
│
├── entity
│   ├── Product.java
│   └── Order.java
│
├── dto
│   ├── ProductReviewDto.java
│   ├── CreateOrderRequest.java
│   └── OrderCreated.java
│
└── EcommerceApplication.java
```

---

# Running the Project

## 1. Clone the Repository

```bash
git clone https://github.com/23-Karthick-B/Ecommerce.git
cd Ecommerce
```

---

## 2. Configure Database

Edit `application.properties`

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce
spring.datasource.username=root
spring.datasource.password=password

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## 3. Run the Application

Using Maven

```bash
mvn spring-boot:run
```

Or run

```
EcommerceApplication.java
```

Server runs at

```
http://localhost:8080
```

---

# API Documentation

Base URL

```
http://localhost:8080/api
```

---

# Product APIs

## Get All Products (Pagination)

```
GET /api/products
```

Query Parameters

| Parameter | Description | Default |
|---|---|---|
| page | Page number | 0 |
| size | Number of products per page | 5 |

Example

```
GET /api/products?page=0&size=5
```

Example Response

```json
{
  "products": [],
  "currentPage": 0,
  "totalItems": 20,
  "totalPages": 4
}
```

---

## Get Product By ID

```
GET /api/products/{id}
```

Example

```
GET /api/products/1
```

Example Response

```json
{
  "id": 1,
  "name": "Laptop",
  "category": "Electronics",
  "price": 50000,
  "rating": 4.5
}
```

---

## Search Products

```
GET /api/products/search
```

Query Parameters

| Parameter | Description |
|---|---|
| category | Filter by category |
| minPrice | Minimum price |
| maxPrice | Maximum price |
| keyword | Search keyword |
| ratings | Filter by rating |

Example

```
GET /api/products/search?category=Electronics&minPrice=10000&maxPrice=50000
```

---

# Product Review API

## Add Product Review

```
POST /api/products/reviews
```

Request Body

```json
{
  "productId": 1,
  "rating": 4,
  "comment": "Good product and worth the price"
}
```

Response

```
Review added
```

---

# Order APIs

## Create Order

```
POST /api/orders
```

Request Body

```json
{
  "productId": 1,
  "quantity": 2,
  "customerName": "John Doe",
  "address": "Mumbai"
}
```

Example Response

```json
{
  "referenceId": "ORD123456",
  "status": "CREATED"
}
```

---

## Get Order By Reference ID

```
GET /api/orders/{referenceId}
```

Example

```
GET /api/orders/ORD123456
```

Example Response

```json
{
  "referenceId": "ORD123456",
  "status": "CREATED",
  "products": [],
  "totalAmount": 50000
}
```

---

# API Testing

You can test the APIs using:

- **Postman**
- **curl**
- **Swagger (if integrated)**

Example endpoint

```
http://localhost:8080/api/products
```

---

# Features Implemented

✔ Product listing with pagination  
✔ Product search with filters  
✔ Product reviews system  
✔ Order creation  
✔ Order retrieval by reference ID  

---

---

# Deployment (AWS)

The application is deployed on **Amazon Web Services (AWS)** using an **EC2 instance**.

## Deployment Architecture

```
Local Development
       ↓
Build JAR using Maven
       ↓
Upload JAR to AWS EC2
       ↓
Run Spring Boot Application
       ↓
Access APIs via Public EC2 IP
```

---

## Steps Used for Deployment

### 1. Launch EC2 Instance

- AWS EC2 instance created
- Operating System: **Ubuntu / Amazon Linux**
- Security group configured to allow:
  - **Port 22 (SSH)**
  - **Port 8080 (Application)**

---

### 2. Install Java on EC2

```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

Verify installation

```bash
java -version
```

---

### 3. Build the Application

On the local machine:

```bash
mvn clean package
```

This generates

```
target/ecommerce.jar
```

---

### 4. Upload JAR to EC2

Using SCP

```bash
scp target/ecommerce.jar ubuntu@<EC2-PUBLIC-IP>:/home/ubuntu
```

---

### 5. Run the Spring Boot Application

SSH into EC2

```bash
ssh ubuntu@<EC2-PUBLIC-IP>
```

Run the application

```bash
java -jar ecommerce.jar
```

---

### 6. Access the API

```
http://<EC2-PUBLIC-IP>:8080/api/products
```

Example:

```
http://54.xx.xxx.xxx:8080/api/products
```

---

## Deployment Benefits

✔ Cloud hosted backend  
✔ Accessible via public API  
✔ Scalable infrastructure  
✔ Demonstrates cloud deployment skills


---

# Author

**Karthick B**

GitHub:  
https://github.com/23-Karthick-B
