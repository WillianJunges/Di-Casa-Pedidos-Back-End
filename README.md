<div align="center">

# 🍽️ Di Casa Pedidos — Back-end

**REST API for an online food ordering system — menu, cart orders, delivery fee by distance and store settings.**

![Java](https://img.shields.io/badge/Java_17-0d1117?style=for-the-badge&logo=openjdk&logoColor=22C55E)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.3-0d1117?style=for-the-badge&logo=springboot&logoColor=22C55E)
![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-0d1117?style=for-the-badge&logo=hibernate&logoColor=22C55E)
![H2](https://img.shields.io/badge/H2_Database-0d1117?style=for-the-badge&logo=databricks&logoColor=22C55E)
![Maven](https://img.shields.io/badge/Maven-0d1117?style=for-the-badge&logo=apachemaven&logoColor=22C55E)
![Google Maps](https://img.shields.io/badge/Google_Maps_API-0d1117?style=for-the-badge&logo=googlemaps&logoColor=22C55E)

</div>

---

## 📖 About

**Di Casa Pedidos** is an ordering system for a homemade-food restaurant: customers browse the menu, build a cart and place
orders for delivery or pickup, while the restaurant manages products, categories, orders and store settings.

This repository contains the **back-end API**. It was built as the Interdisciplinary Project (PI) of the
4th semester of Systems Analysis and Development at **FATEC**, as a team project.
The front-end lives in [Di-Casa-Pedidos-Front-End](https://github.com/Murilo-Bioni-Caruso/Di-Casa-Pedidos-Front-End).

## ✨ Features

- 🍲 **Menu management** — CRUD for products and categories (with emoji icons)
- 🧾 **Orders** — items, subtotal, delivery fee, total, payment method, change, delivery/pickup and scheduled time
- 👤 **Users & login** — customer registration and login endpoint (password removed from the login response)
- 📍 **Delivery distance** — calculates the distance between the store and the customer using the Google Maps Distance Matrix API
- 🏪 **Store settings** — address, contact, coordinates, opening hours and PIX keys
- 🖼️ **Image upload** — upload product images (up to 10 MB)
- 🌱 **Seed data** — default admin, categories, products and settings created on first run
- ⚠️ **Global exception handling** — consistent error responses

## 🔌 API Endpoints

| Resource | Method | Endpoint | Description |
|---|---|---|---|
| Products | `GET` `POST` | `/produtos` | List / create products |
| | `PUT` `DELETE` | `/produtos/{id}` | Update / delete a product |
| Categories | `GET` | `/categorias` · `/categorias/todas` | List categories |
| | `POST` | `/categorias` | Create a category |
| | `PUT` `DELETE` | `/categorias/{id}` | Update / delete a category |
| Orders | `GET` `POST` | `/pedidos` | List / create orders |
| | `PUT` | `/pedidos/{id}` | Update an order (e.g. status) |
| Users | `GET` `POST` | `/usuarios` | List / register users |
| | `PUT` | `/usuarios/{id}` | Update a user |
| | `POST` | `/usuarios/login` | Log in |
| Settings | `GET` `PUT` | `/configuracoes` | Get / update store settings |
| Maps | `GET` | `/maps/distancia?endereco=` | Distance from the store to an address |
| Upload | `POST` | `/upload` | Upload an image |

## 🧱 Architecture

```
Controller  →  Service  →  Repository (Spring Data JPA)  →  H2 (file database)
```

- Layered architecture: controllers handle HTTP, services hold the business rules, repositories access the database.
- Flexible fields (order items, opening hours, PIX keys) are stored as JSON using custom JPA `AttributeConverter`s.
- H2 runs in **file mode**, so data persists between restarts.

## 🚀 Getting Started

**Requirements:** Java 17+

```bash
./mvnw spring-boot:run
```

The API starts at `http://localhost:8080`.

- **H2 console:** `http://localhost:8080/h2-console` (JDBC URL `jdbc:h2:file:./data/dicasa-db`, user `sa`, no password)
- **Default admin (local dev):** `admin` / `admin`
- **Google Maps (optional):** set the `GOOGLE_MAPS_API_KEY` environment variable to enable the distance endpoint

## ⚠️ Known Limitations

This is an academic project and is not production-ready:

- Passwords are stored in plain text (no hashing yet) and there is no token-based authentication.
- `GET /usuarios` still returns user credentials and endpoints are not protected by roles.
- CORS allows any origin to make local development easier.

---

<div align="center">

Made with 🟢 by [Willian Thiago Junges](https://github.com/WillianJunges) and team

</div>
