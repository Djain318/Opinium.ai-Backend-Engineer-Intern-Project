# Data Transformation Pipeline

## 🚀 Deployment

**Live API Base URL:** [https://opinium-ai-backend-engineer-intern.onrender.com/](https://opinium-ai-backend-engineer-intern.onrender.com/)

## 🚀 Overview

This project implements a data transformation pipeline that fetches raw event data from multiple public APIs, normalizes and enriches it using business rules, and provides an API to query the processed data.

## 🚀 Features

- Fetches data from three public sources:
  - E-commerce product data
  - User data
  - Transaction/order data
- Transforms and normalizes data into a unified format.
- Applies business rules:
  - Joins transaction data with product data to include product details.
  - Joins transaction data with user data for complete purchase records.
  - Calculates total spending per user.
  - Identifies the most popular product categories.
  - Computes the average transaction value.
- Provides FastAPI-based endpoints for querying processed data.

## 🚀 Data Sources

The following public APIs are used:

**1️⃣ Products API**: [FakeStoreAPI](https://fakestoreapi.com/products)

- Endpoint: `https://fakestoreapi.com/products`
- Represents the product catalog.

**2️⃣ Users API**: [RandomUser API](https://randomuser.me/api/?results=20)

- Endpoint: `https://randomuser.me/api/?results=20`
- Represents user profiles.

**3️⃣ Transactions API**: [Mockaroo API](https://my.api.mockaroo.com/orders.json?key=e49e6840)

- Endpoint: `https://my.api.mockaroo.com/orders.json?key=e49e6840`
- Represents purchase transactions.

## 🚀 Data Transformation

All fetched data is transformed into the following standardized format:

```json
{
    "entity_id": "generated-unique-id",
    "entity_type": "product|user|transaction",
    "timestamp": "ISO-8601-format",
    "data": {
      "//Normalized fields from the source"
    },
    "metadata": {
        "source": "which API",
        "processed_at": "processing timestamp"
    }
}
```

## 🚀 API Endpoints

### **1️⃣ Retrieve Processed Data**

```http
GET /data/{entity_type}
```

- Fetches processed data based on entity type (`product`, `user`, or `transaction`).
- Hosted API Endpoint:
  [https://opinium-ai-backend-engineer-intern.onrender.com/data/{entity\_type}](https://opinium-ai-backend-engineer-intern.onrender.com/data/{entity_type})

### **2️⃣ User Spending Insights**

```http
GET /insights/users
```

- Returns total spending per user.
- Hosted API Endpoint:
  [https://opinium-ai-backend-engineer-intern.onrender.com/insights/users](https://opinium-ai-backend-engineer-intern.onrender.com/insights/users)

### **3️⃣ Product Popularity Insights**

```http
GET /insights/products
```

- Identifies the most popular product categories.
- Hosted API Endpoint:
  [https://opinium-ai-backend-engineer-intern.onrender.com/insights/products](https://opinium-ai-backend-engineer-intern.onrender.com/insights/products)

### **4️⃣ Test the Endpoints Using Swagger UI**

FastAPI provides an interactive API documentation using Swagger UI. Once the server is running:

- Open your browser and go to: `http://127.0.0.1:8000/docs`
- You can interact with all the API endpoints directly from this interface.

Alternatively, you can use Redoc:

- Open `http://127.0.0.1:8000/redoc`

#### Swagger UI Preview

## 🚀 Project Setup Instructions

### **1️⃣ Clone the Repository**

```sh
git clone https://github.com/Djain318/Opinium.ai-Backend-Engineer-Intern-Project.git
cd Opinium.ai-Backend-Engineer-Intern-Project
```

### **2️⃣ Create a Virtual Environment**

```sh
python -m venv .venv
```

On Windows:

```sh
.venv\Scripts\activate
```

On macOS/Linux:

```sh
source .venv/bin/activate
```

### **3️⃣ Install Dependencies**

```sh
pip install -r requirements.txt
```

### **4️⃣ Run the Application**

```sh
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

