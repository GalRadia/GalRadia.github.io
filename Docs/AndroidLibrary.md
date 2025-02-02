# Inventory Management Library

## Overview

The Inventory Management Library is designed to help manage inventory items, transactions, and users. It provides functionalities to add, update, remove items, fetch transactions, and generate bar chart data for trends.
The library is built using java and communicates with the backend API with Vercel.

## Setup
Refer to the [Setup Guide](/Docs/Setup.md#android-library-setup) for detailed instructions on setting up the project. 


## Installation

Add the following dependency to your `build.gradle` file:

```gradle
dependencies {
	        implementation 'com.github.GalRadia:InventoryManagement:Tag'
	}
```

## Features

- **Item Management**:
  - Add, update, and remove inventory items.
  - Fetch details of a single item or all items.
  - Search for items by name.
  
- **Transaction Management**:
  - Record transactions, specifying item and quantity.
  - Fetch all transactions or filter transactions by user.
  
- **User Management**:
  - User registration with username, password, and role.
  - User login and JWT authentication.
  - Fetch active users and manage user roles.
  
- **Trend Analysis**:
  - Fetch trending items based on sales and revenue for a given period.
  - Generate bar chart data to visualize item trends.
  
- **Authentication**:
  - JWT-based authentication with automatic token refresh.
  - Token expiration handling and automatic invalidation.
  
- **Flexible Data Handling**:
  - Fetch data using Retrofit calls or LiveData.
  - Use with **MPAndroidChart** to generate visualizations of trends.

## Usage
    
### Initialization

```java
InventoryManagement inventoryManagement = InventoryManagement(context)
``` 

You can now use the SDK's methods to manage items, transactions, and users.

### Item Management

- **Get Item by ID**:

  Use `LiveData` or Retrofit calls to fetch an item by its ID.

  ```java
  inventoryManagement.getItemByIdAsLiveData("itemId");
  inventoryManagement.getItemByIdCall("itemId");
  ```

- **Insert an Item**:

  Add a new item to the inventory:

  ```java
  inventoryManagement.insertItem("Item Name", 10, 50.0f, "Item Description");
  inventoryManagement.insertItemCall("Item Name", 10, 50.0f, "Item Description");
  ```

- **Update an Item**:

  Update an existing item in the inventory:

  ```java
  Item updatedItem = new Item("Updated Name", 15, 55.0f, "Updated Description");
  inventoryManagement.updateItem("itemId", updatedItem);
  inventoryManagement.updateItemCall("itemId", updatedItem);
  ```

- **Remove an Item**:

  Remove an item from the inventory:

  ```java
  inventoryManagement.removeItem("itemId");
  inventoryManagement.removeItemCall("itemId");
  ```

### Transaction Management

- **Record a Transaction**:

  Create a transaction for a specified item:

  ```java
  inventoryManagement.insertTransaction("itemId", 5); // 5 items sold
  inventoryManagement.insertTransactionCall("itemId", 5); 
  ```

- **Fetch All Transactions**:

  Retrieve all transactions:

  ```java
  inventoryManagement.getAllTransactions();
  inventoryManagement.getAllTransactionsCall();
  ```

- **Fetch Transactions by User**:

  Get all transactions for the current user:

  ```java
  inventoryManagement.getTransactionsByUser();
  inventoryManagement.getTransactionsByUserCall();
  ```

### User Management

- **Register a New User**:

  Register a user with a specified role (e.g., admin, manager):

  ```java
  inventoryManagement.register("username", "password", "role");
  inventoryManagement.registerCall("username", "password", "role");
  ```

- **Login**:

  Authenticate a user with username and password:

  ```java
  inventoryManagement.login("username", "password");
  ```

- **Get Active Users**:

  Retrieve all active users in the system:

  ```java
  inventoryManagement.getActiveUsers();
  ```

### Trend Analysis

- **Get Trending Items**:

  Fetch trending items based on sales and revenue:

  ```java
  inventoryManagement.getTrending(10, 30); // Get top 10 trending items in the last 30 days
  inventoryManagement.getTrendingCall(10, 30);
  ```

- **Generate Bar Chart Data**:

  Use the **MPAndroidChart** library to visualize trends:

  ```java
  BarData barData = inventoryManagement.getBarChartData(trends);
  ```

### Authentication

The SDK uses JWT tokens for authentication. It includes functionality for refreshing expired tokens automatically.

- **Refresh Token**:

  Refresh the authentication token when expired:

  ```java
  inventoryManagement.refreshToken();
  ```

### Utility Methods

- **Check if User is a Manager**:

  Determine if the logged-in user has manager privileges:

  ```java
  inventoryManagement.isManager();
  ```

## Example Code

Here is an example of using the SDK to register a user and fetch all items:

```java
InventoryManagement inventoryManagement = InventoryManagement.getInstance(context);

// Register a user
inventoryManagement.register("john_doe", "password123", "manager");

// Fetch all items
inventoryManagement.getAllItemsAsLiveData().observe(this, items -> {
    // Handle items here
});
```

## Dependencies

- **MPAndroidChart** for generating bar charts.
- **Retrofit** for making API calls.

<img src="https://github.com/user-attachments/assets/3c374fb7-f350-466e-ba40-9317bad37221" width="500">

<img src="https://github.com/user-attachments/assets/27b951b4-e61f-4a42-8aae-fafe3bd21b38" width="500">

<img src="https://github.com/user-attachments/assets/4a3d35da-0f80-4ec0-bd58-a875273f6af2" width="500">

<img src="https://github.com/user-attachments/assets/c5a369f1-4b0c-465c-8c44-ad6168bd8586" width="500">

