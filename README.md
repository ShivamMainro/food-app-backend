# Food App Backend

This is a **Node.js + Express + MongoDB** backend project for a food delivery app. It supports user authentication, restaurant management, food items, categories, and order placement.

---

## Base URL

http://localhost:8080/api/v1/


---

## Table of Contents

1. [Auth Routes](#auth-routes)
2. [User Routes](#user-routes)
3. [Category Routes](#category-routes)
4. [Food Routes](#food-routes)
5. [Restaurant Routes](#restaurant-routes)
6. [Middlewares](#middlewares)

---

## Auth Routes

### 1. Register User
**POST** `/auth/register`  
**Body (JSON):**
```json
{
  "userName": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "1234567890",
  "address": ["Street, City, Country"],
  "answer": "Your security answer"
}

2. Login User

POST /auth/login
Body (JSON):

{
  "email": "john@example.com",
  "password": "password123"
}

User Routes (Requires Auth)
1. Get User Info

GET /user/getUser
Headers: Authorization: Bearer <token>

2. Update Profile

PUT /user/updateUser
Body (JSON):

{
  "userName": "John Doe",
  "phone": "9876543210",
  "address": ["New Street, City, Country"]
}

3. Update Password

POST /user/updatePassword
Body (JSON):

{
  "oldPassword": "password123",
  "newPassword": "newpassword456"
}

4. Reset Password

POST /user/resetPassword
Body (JSON):

{
  "email": "john@example.com",
  "answer": "Your security answer",
  "newPassword": "newpassword456"
}

5. Delete Profile

DELETE /user/deleteUser/:id

Category Routes
1. Create Category

POST /category/create (Auth Required)
Body (JSON):

{
  "title": "Pizza",
  "imageUrl": "https://link-to-image.png"
}

2. Get All Categories

GET /category/getAll

3. Update Category

PUT /category/update/:id (Auth Required)
Body (JSON):

{
  "title": "Updated Category Title",
  "imageUrl": "https://updated-image.png"
}

4. Delete Category

DELETE /category/delete/:id (Auth Required)

Food Routes
1. Create Food

POST /food/create (Auth Required)
Body (JSON):

{
  "title": "Chicken Pizza",
  "description": "Delicious cheesy chicken pizza",
  "price": 5,
  "imageUrl": "https://image.png",
  "foodTags": "spicy",
  "catgeory": "Pizza",
  "code": "1234",
  "isAvailabe": true,
  "resturnat": "restaurant_id_here",
  "rating": 5
}

2. Get All Foods

GET /food/getAll

3. Get Single Food

GET /food/get/:id

4. Get Food by Restaurant

GET /food/getByResturant/:id

5. Update Food

PUT /food/update/:id (Auth Required)
Body (JSON): (similar to create food)

6. Delete Food

DELETE /food/delete/:id (Auth Required)

7. Place Order

POST /food/placeorder (Auth Required)
Body (JSON):

{
  "cart": [
    { "_id": "food_id_here", "price": 5 },
    { "_id": "food_id_here2", "price": 7 }
  ]
}

8. Change Order Status

POST /food/orderStatus/:id (Auth + Admin)
Body (JSON):

{
  "status": "on the way"
}

Restaurant Routes
1. Create Restaurant

POST /resturant/create (Auth Required)
Body (JSON):

{
  "title": "Burger King",
  "imageUrl": "https://image.png",
  "foods": [],
  "time": "9am to 9pm",
  "pickup": true,
  "delivery": true,
  "isOpen": true,
  "logoUrl": "https://logo.png",
  "rating": 5,
  "ratingCount": "5",
  "code": "1234",
  "coords": {
    "id": "123",
    "latitude": 12.34,
    "latitudeDelta": 0.01,
    "longitude": 56.78,
    "longitudeDelta": 0.01,
    "address": "City, Country"
  }
}

2. Get All Restaurants

GET /resturant/getAll

3. Get Restaurant by ID

GET /resturant/get/:id

4. Delete Restaurant

DELETE /resturant/delete/:id (Auth Required)

Middlewares

authMiddleware – Validates JWT token and attaches user ID to request.

adminMiddleware – Checks if user is admin (used in order status route).

Notes

Use POSTMAN or Insomnia to test API routes.

Include Authorization header for protected routes:

Authorization: Bearer <your_jwt_token_here>
