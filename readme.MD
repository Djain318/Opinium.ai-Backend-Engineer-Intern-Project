# Data Transformation Pipeline

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8%2B-blue" alt="Python Version">
  <img src="https://img.shields.io/badge/FastAPI-0.95.0-green" alt="FastAPI Version">
  <img src="https://img.shields.io/badge/uvicorn-0.23.0-orange" alt="Uvicorn Version">
</p>

## Overview

This project implements a data transformation pipeline that fetches raw event data from multiple public APIs, normalizes and enriches it using business rules, and provides an API to query the processed data.

## Features

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

## Data Sources

The following public APIs are used:

1. **Products API**: [FakeStoreAPI](https://fakestoreapi.com/products)
   - Endpoint: `https://fakestoreapi.com/products`
   - Represents the product catalog.
2. **Users API**: [RandomUser API](https://randomuser.me/api/?results=20)
   - Endpoint: `https://randomuser.me/api/?results=20`
   - Represents user profiles.
3. **Transactions API**: [Mockaroo API](https://my.api.mockaroo.com/orders.json?key=e49e6840)
   - Endpoint: `https://my.api.mockaroo.com/orders.json?key=e49e6840`
   - Represents purchase transactions.

## Data Transformation

All fetched data is transformed into the following standardized format:

```json
{
    "entity_id": "generated-unique-id",
    "entity_type": "product|user|transaction",
    "timestamp": "ISO-8601-format",
    "data": {
        // Normalized fields from the source
    },
    "metadata": {
        "source": "which API",
        "processed_at": "processing timestamp"
    }
}
```

## API Endpoints

### **1. Retrieve Processed Data**

```http
GET /data/{entity_type}
```

- Fetches processed data based on entity type (`product`, `user`, or `transaction`).
- Example request:
  ```http
  GET /data/product
  ```

### **2. User Spending Insights**

```http
GET /insights/users
```

- Returns total spending per user.
- Example response:
  ```json
  {
      "user_spending": {
          "1234567890": 120.5,
          "0987654321": 200.75
      }
  }
  ```

### **3. Product Popularity Insights**

```http
GET /insights/products
```

- Identifies the most popular product categories.
- Example response:
  ```json
  {
      "most_popular_category": "electronics",
      "purchase_count": 45,
      "category_data": {
          "electronics": 45,
          "clothing": 30,
          "home": 20
      }
  }
  ```

## Project Setup Instructions

### **1. Clone the Repository**

```sh
git clone <repository-url>
cd <repository-name>
```

### **2. Create a Virtual Environment** (optional but recommended)

```sh
python -m venv .venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate
```

### **3. Install Dependencies**

Ensure you have Python installed (version 3.8+ recommended). Then, install dependencies:

```sh
pip install -r requirements.txt
```

### **4. Run the Application**

Execute the following command to start the FastAPI server:

```sh
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### **5. Test the Endpoints Using Swagger UI**

FastAPI provides an interactive API documentation using Swagger UI. Once the server is running:

- Open your browser and go to: `http://127.0.0.1:8000/docs`
- You can interact with all the API endpoints directly from this interface.

Alternatively, you can use Redoc:

- Open `http://127.0.0.1:8000/redoc`

## File Structure

```
📂 project_root/
├── 📂 .venv/               # Virtual environment (optional)
├── 📂 app/
│   ├── apicalling.py      # Functions to fetch and transform data
├── main.py                # FastAPI application entry point
├── .gitignore             # Git ignore file
├── README.md              # Documentation
├── requirements.txt       # Dependencies
```

## Approach Summary

1. **Data Ingestion**: Fetches data from the three public APIs.
2. **Data Transformation**: Converts raw data into a standardized JSON format.
3. **Data Enrichment**:
   - Transactions are linked with products and users.
   - User spending is calculated.
   - Product category popularity is analyzed.
4. **API Development**: Implements FastAPI endpoints to expose processed data and insights.

## Error Handling

- **API failures**: Uses exception handling (`try-except`) to catch request errors.
- **Missing data**: Uses default values and empty structures to avoid crashes.

## Future Enhancements

- Implement persistent storage (e.g., SQLite, PostgreSQL) for better scalability.
- Introduce caching mechanisms to optimize API response time.
- Implement authentication and authorization mechanisms for data security.

## Contact

For any queries, reach out to `chetan@opinium.ai`.

---

This README provides an overview, setup guide, API documentation, and a brief implementation summary to help understand and run the project effectively.

