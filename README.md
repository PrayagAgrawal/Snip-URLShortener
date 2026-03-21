# 🔗 Snip – URL Shortener with Analytics & JWT Auth

Snip is a backend service that allows users to create short URLs, track engagement through analytics, and securely manage their links using JWT-based authentication.

Built with **Spring Boot**, **Spring Security**, and **JPA**, this project demonstrates real-world backend architecture, including authentication, REST APIs, and data analytics.

> A production-style backend system demonstrating secure authentication, scalable API design, and real-time analytics.

---

## 📱 Feature Overview

* 🔐 **Authentication & Security**

  * User registration and login using JWT
  * Stateless authentication with Spring Security
  * Password encryption using BCrypt

* 🔗 **URL Shortening**

  * Generate unique short URLs for long links
  * Store mappings with user association

* 🔁 **Redirection & Tracking**

  * Redirect short URLs to original links (HTTP 302)
  * Record each visit as a ClickEvent
  * Maintain total click count per URL

* 📊 **Analytics**

  * Track every click with timestamp
  * Aggregate clicks date-wise using Java Streams
  * Fetch per-URL analytics within a date range
  * Retrieve total clicks across all user URLs

* 🧱 **Scalable Architecture**

  * Layered design (Controller → Service → Repository)
  * Clean separation of concerns
  * DTO-based API responses

---

## 🏗️ Architecture Overview

The application follows a layered architecture with JWT-based security for handling requests efficiently and securely.

### 🔄 Request Flow

1. Client sends request with JWT token
2. **JWT Filter** validates token and sets authentication context
3. Request reaches **Controller Layer** (API endpoints)
4. **Service Layer** processes business logic
5. **Repository Layer** interacts with the database
6. Response is returned to the client

### 🔐 Security Layer

* Stateless authentication using JWT
* Requests are filtered before reaching controllers
* Protected endpoints require valid authentication

---

## 🔗 API Endpoints

### 🔐 Authentication

#### ➕ Register

```
POST /api/auth/public/register
```

**Request Body**

```json
{
  "username": "john",
  "email": "john@example.com",
  "password": "123456"
}
```

---

#### 🔓 Login

```
POST /api/auth/public/login
```

**Request Body**

```json
{
  "username": "john",
  "password": "123456"
}
```

**Response**

```json
{
  "token": "JWT_TOKEN"
}
```

---

### 🔗 URL Management (Requires JWT)

> Include header:

```
Authorization: Bearer <JWT_TOKEN>
```

---

#### ➕ Create Short URL

```
POST /api/urls/shorten
```

**Request Body**

```json
{
  "originalUrl": "https://example.com"
}
```

**Sample Response**

```json
{
  "id": 1,
  "originalUrl": "https://example.com",
  "shortUrl": "AbC123xY",
  "clickCount": 0,
  "createdDate": "2026-03-21T12:00:00",
  "username": "prayag"
}
```

---

#### 📄 Get User URLs

```
GET /api/urls/myurls
```

---

#### 📊 Get URL Analytics

```
GET /api/urls/analytics/{shortUrl}?startDate=2024-01-01T00:00:00&endDate=2024-01-10T23:59:59
```

---

#### 📈 Get Total Clicks

```
GET /api/urls/totalClicks?startDate=2024-01-01&endDate=2024-01-10
```

---

### 🔁 Redirect

```
GET /{shortUrl}
```

* Redirects to original URL (HTTP 302)
* Records click event for analytics

---

## 📸 API Demo (Postman)

### 🔐 Login – JWT Authentication

<img src="/media/Login.png" alt="Login API" width="700"/>

---

### 🔗 Create Short URL

<img src="/media/Shorten.png" alt="Create URL API" width="700"/>

---

### 🔐 Request Headers

<img src="/media/Auth-header.png" width="700"/>

---

### 📊 URL Analytics

<img src="/media/Analytics.png" alt="Analytics API" width="700"/>

---

## 📦 Project Structure

```
com.urlshortener
│
├── controller     # Handles REST API requests (Auth, URL operations)
├── service        # Contains core business logic
├── repository     # JPA repositories for database access
├── models         # Entity classes (User, UrlMapping, ClickEvent)
├── dtos           # Data Transfer Objects for API communication
├── security       # JWT utilities, filters, and security configuration
```

---

## 🧱 Data Model Overview

The system is designed using relational entities with clear associations to support URL management and analytics.

* 👤 **User → UrlMapping (One-to-Many)**
  A user can create multiple shortened URLs.

* 🔗 **UrlMapping → ClickEvent (One-to-Many)**
  Each URL tracks multiple click events for analytics.

* 📊 **ClickEvent**
  Stores timestamped records of every URL access, enabling date-wise analysis.

### 🔍 Design Highlights

* Normalized structure to avoid data redundancy
* Efficient analytics using event-based tracking
* Supports scalable aggregation (per URL and per user)

---

## 🛠️ Tech Stack

| Category       | Technology            |
| -------------- | --------------------- |
| **Backend**    | Spring Boot           |
| **Security**   | Spring Security + JWT |
| **Database**   | MySQL                 |
| **ORM**        | JPA (Hibernate)       |
| **Language**   | Java                  |
| **Build Tool** | Maven                 |
| **API Style**  | REST                  |

---

## 🧑‍💻 Author

**Prayag Agrawal**

* 💼 LinkedIn: https://www.linkedin.com/in/prayag-agrawal
