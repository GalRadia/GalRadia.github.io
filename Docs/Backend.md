
# Backend Documentation

## Overview
The backend is built using **Flask** and **pymongo** for database operations.
It provides a RESTful API for an inventory management system. It includes authentication, inventory management, and transaction handling. The API uses JWT for authentication and role-based access control for manager-restricted actions.
The backend is hosted on Vercel.

For every request, the client must include a valid JWT token in the `Authorization` header as `Bearer <TOKEN>`. The token is generated during login and must be refreshed periodically (1 hour).
## Setup
learn how to setup the backend in the [Setup Guide](Setup.md#backend-setup).
## API Endpoints
The backend provides the following API endpoints:

[Authentication](#authentication) - Register, login, and manage users.

[Inventory](#inventory) - Manage inventory items.

[Transactions](#transactions) - Process purchases and view transaction history.

## Authentication

### `POST auth/login`
**Description:** Logs in a user and returns a JWT token.
**Request Body:**
```json
{
  "username": "user1",
  "password": "securepassword"
}
```
**Response:**
```json
{
  "message": "Login successful",
  "token": "<JWT_TOKEN>",
  "role": "user"
}
```

### `POST auth/register`
**Description:** Registers a new user. role can be either `user` or `manager`.
**Request Body:**
```json
{
  "username": "user1",
  "password": "securepassword",
  "role": "user"
}
```
**Response:**
```json
{
  "message": "User registered successfully"
}
```
### PUT `auth/refresh-token`
**Description:** Refreshes the JWT token.
**Response:**
```json
{
  "message": "Token refreshed successfully
}
```
### GET `auth/active`
**Description:** Get a list of all active users by jwt. 
**Response:**
```json
{
   [
    {
      "username": "user1",
      "role": "user"
    },
    {
      "username": "manager1",
      "role": "manager"
    }
    ]
}
```
### GET `auth/users`
**Description:** Get a list of all users.
**Response:**
```json
{
   [
    {
      "username": "user1",
      "role": "user"
    },
    {
      "username": "manager1",
      "role": "manager"
    }
    ]
}
```
### GET `auth/users/<username>`
**Description:** Get a user by username.
**Response:**
```json
{
  "username": "user1",
  "role": "user"
}
``` 
### DELETE `auth/users/<username>`
**Description:** Delete a user by username.(Manager Only)
**Response:**
```json
{
  "message": "User deleted successfully"
}
```
### GET `/audit/exp`
**Description:** Get a expiration time of the jwt. (All timestamps are in UTC)
**Response:**
```json

    "exp": "2025-02-02T12:00:00Z"

}
```
## Inventory

### `GET inventory/items`
**Description:** Retrieves all inventory items.
**Response:**
```json
[
  {
    "_id": "64a9b1234567",
    "name": "Laptop",
    "quantity": 10,
    "price": 1000.0
  },
    {
        "_id": "64a9b1234568",
        "name": "Mouse",
        "quantity": 20,
        "price": 20.0
    }
]
```

### `GET inventory/items/<item_id>`
**Description:** Retrieves an item by its ID.
**Response:**
```json
{
  "_id": "64a9b1234567",
  "name": "Laptop",
  "quantity": 10,
  "price": 1000.0
}
```

### `GET inventory/search?name=<item_name>`
**Description:** Searches for an item by name.
**Response:**
```json
[
  {
    "_id": "64a9b1234567",
    "name": "Laptop",
    "quantity": 10,
    "price": 1000.0
  }
]
```

### `POST /insert_item` (Manager Only)
**Description:** Adds a new item to the inventory.
**Request Body:**
```json
{
  "name": "Laptop",
  "quantity": 10,
  "price": 1000.0
}
```
**Response:**
```json
{
  "message": "Item inserted successfully",
  "item_id": "64a9b1234567"
}
```

### `PUT /update_item/<item_id>` (Manager Only)
**Description:** Updates an existing inventory item.
**Request Body:**
```json
{
  "quantity": 15,
  "price": 950.0
}
```
**Response:**
```json
{
  "message": "Item updated successfully"
}
```

### `DELETE /remove/<item_id>` (Manager Only)
**Description:** Deletes an inventory item.
**Response:**
```json
{
  "message": "Item deleted successfully"
}
```

## Transactions

### `POST transaction/purchase`
**Description:** Processes a purchase transaction.
**Request Body:**
```json
{
  "item_id": "64a9b1234567",
  "quantity": 2
}
```
**Response:**
```json
{
  "message": "Transaction completed successfully"
}
```

### `GET /transactions` (Manager Only)
**Description:** Retrieves all transactions.
**Response:**
```json
[
  {
    "transaction_id": "txn123",
    "item_name": "Laptop",
    "quantity": 2,
    "buyer": "user1",
    "timestamp": "2025-02-02T12:00:00Z"
  }
]
```

### `GET /transactions/mine`
**Description:** Retrieves the transactions made by the authenticated user.
**Response:**
```json
[
  {
    "transaction_id": "txn123",
    "item_name": "Laptop",
    "quantity": 2,
    "buyer": "user1",
    "timestamp": "2025-02-02T12:00:00Z"
  }
]
```

### `GET /trending`
**Description:** Retrieves the trending items based on sales in the last N days.
**Query Parameters:**
- `days`: Number of days to look back (default: 7)
- `limit`: Number of top-selling items to return (default: 10)

**Response:**
```json
[
  {
    "item_id": "64a9b1234567",
    "item_name": "Laptop",
    "total_sales": 5,
    "total_revenue": 5000.0
  }
]
```

## Authorization

### JWT Authentication
- The backend uses JWT authentication.
- A valid token must be included in the `Authorization` header as `Bearer <TOKEN>`.

### Role-based Access Control
- Managers can add, update, and remove items.
- Users can purchase items and view their transaction history.

## Error Handling
- `401 Unauthorized`: Missing or invalid token.
- `403 Forbidden`: User lacks permission.
- `404 Not Found`: Resource does not exist.
- `400 Bad Request`: Invalid request format.
- `500 Internal Server Error`: Unexpected error.

## Notes
- All dates and timestamps are in UTC.
- The API returns JSON responses.
- `manager_required` decorator restricts access to manager-only endpoints.

