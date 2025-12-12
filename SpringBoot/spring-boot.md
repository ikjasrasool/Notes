

# **REST API (Representational State Transfer API)**

A **REST API** is an architectural style for designing networked applications that allows different software systems to communicate with each other over the internet. It uses standard **HTTP methods** and exchanges data in lightweight formats like **JSON**.

---

## **Key Concepts**

### **API (Application Programming Interface)**

A set of rules that defines how one application interacts with another. It acts as a messenger between:

* **Client** → the application making the request
* **Server** → the application providing the data or service

### **REST (Representational State Transfer)**

An architectural style (not a protocol) that promotes:

* Simple communication
* Stateless interactions
* Uniform access to resources

### **Resources**

Everything in REST is a **resource**, such as:

* A user profile
* An order
* An image

Each resource has a unique **URI** (like `/users/123`).

---

## **How It Works**

REST APIs use standard **HTTP methods** to perform actions:

| Method     | Description                       | Example                         |
| ---------- | --------------------------------- | ------------------------------- |
| **GET**    | Retrieve a resource               | `/users/123` (Get user details) |
| **POST**   | Create a new resource             | `/users` (Create new user)      |
| **PUT**    | Update/replace an entire resource | `/users/123`                    |
| **PATCH**  | Update partial resource           | `/users/123`                    |
| **DELETE** | Delete a resource                 | `/users/123`                    |

The **client** sends a request → the **server** processes it → server sends a response with:

* HTTP Status Code (e.g., **200 OK**, **404 Not Found**)
* Data (usually JSON)

---

## **Benefits of REST API**

### **1. Scalability**

REST is stateless, meaning the server does not store client session data. This allows easy distribution of requests across servers.

### **2. Flexibility**

Supports multiple data formats:

* JSON
* XML
* HTML

Clients and servers can use different programming languages.

### **3. Simplicity**

Uses:

* Standard web methods
* Human-readable URIs
* Easy-to-learn conventions

---

## **Common Examples of REST APIs**

### **1. User Management**

* **GET** `/users` → Get list of all users
* **POST** `/users` → Create a new user
* **GET** `/users/10` → Get details of user with ID 10
* **PATCH** `/users/10` → Update user's email
* **DELETE** `/users/10` → Delete user

---

### **2. E-Commerce API**

* **GET** `/products` → List all products
* **GET** `/products/45` → Product details
* **POST** `/orders` → Create an order
* **GET** `/orders/123` → View order status
* **DELETE** `/cart/5` → Remove item from cart

---

### **3. Social Media API**

* **POST** `/posts` → Create a post
* **GET** `/posts` → View all posts
* **GET** `/posts/55/comments` → Get comments on a post
* **POST** `/posts/55/like` → Like a post

---

### **4. Weather API**

* **GET** `/weather?city=Chennai` → Get current weather
* **GET** `/forecast?city=Delhi` → Get 7-day weather forecast

---

### **5. Banking/Payments API**

* **POST** `/transactions` → Start a transaction
* **GET** `/transactions/987` → Check transaction status
* **GET** `/balance` → Get account balance

---
