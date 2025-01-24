

# **FastAPI Role-Based Access Control Project**



This project is a FastAPI-based application with role-based permissions for users. It includes two main entities: **Users** and **Products**. The application uses **PostgreSQL** as the database and provides role-specific access control for admins, managers, and users.

---

## **Features**

### **User Roles and Permissions**
- **Admin**: Full access (view, create, update, and delete operations).
- **Manager**: Access to view and create records only.
- **User**: Read-only access to data.

### **Endpoints**
- **Users**:
  - View all users (Admin, Manager, User).
  - Create a user (Admin, Manager).
  - Delete a user (Admin only).
- **Products**:
  - View all products (Admin, Manager, User).
  - Create a product (Admin, Manager).

### **Database**
- PostgreSQL integration.
- Table schemas:
  - **User Table**: Stores user details (username, email, password, and role).
  - **Product Table**: Stores product details (name, price, description).

### **Security**
- Role-based permissions using FastAPI dependencies.
- Mocked role-based access (to be replaced with proper authentication logic).

---

## **Folder Structure**

```
fastapi_project/
│
├── app/
│   ├── core/
│   │   ├── config.py        # Application configuration
│   │   ├── database.py      # Database connection
│   │
│   ├── models/
│   │   ├── user.py          # User model
│   │   ├── product.py       # Product model
│   │
│   ├── routers/
│   │   ├── user.py          # User endpoints
│   │   ├── product.py       # Product endpoints
│   │
│   ├── schemas/
│   │   ├── user.py          # User schemas
│   │   ├── product.py       # Product schemas
│   │
│   ├── utils/
│   │   ├── permissions.py   # Role-based permission utilities
│   │
│   ├── __init__.py
│   ├── main.py              # Application entry point
│
├── .env                     # Environment variables
├── requirements.txt         # Python dependencies
├── alembic/                 # Database migrations
└── README.md                # Project documentation
```

---

## **Setup Instructions**

### **Prerequisites**
- Python 3.9 or higher
- PostgreSQL installed and running
- A database created in PostgreSQL (e.g., `mydb`)

### **Installation**

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/fastapi-rbac.git
   cd fastapi-rbac
   ```

2. Create a virtual environment:
   ```bash
   python -m venv env
   source env/bin/activate  # On Windows: env\Scripts\activate
   ```

3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Configure the `.env` file:
   Create a `.env` file in the root directory and add the following:
   ```
   DATABASE_URL=postgresql+psycopg2://<username>:<password>@localhost:5432/<database>
   SECRET_KEY=your-secret-key
   ```
   Replace `<username>`, `<password>`, and `<database>` with your PostgreSQL credentials.

5. Run database migrations (optional, if using Alembic):
   ```bash
   alembic upgrade head
   ```

6. Start the application:
   ```bash
   uvicorn app.main:app --reload
   ```

---

## **API Endpoints**

### **Base URL**
`http://127.0.0.1:8000`

### **Users**
| Method | Endpoint    | Description               | Role Permissions             |
|--------|-------------|---------------------------|------------------------------|
| GET    | `/users/`   | Get all users            | Admin, Manager, User         |
| POST   | `/users/`   | Create a new user        | Admin, Manager               |
| DELETE | `/users/{id}` | Delete a user by ID     | Admin                        |

### **Products**
| Method | Endpoint      | Description               | Role Permissions             |
|--------|---------------|---------------------------|------------------------------|
| GET    | `/products/`  | Get all products         | Admin, Manager, User         |
| POST   | `/products/`  | Create a new product     | Admin, Manager               |

---

## **Testing the Application**

1. Use a tool like Postman or cURL to test the endpoints.

2. **Example Requests**:
   - **Get Users**:
     ```bash
     curl -X GET http://127.0.0.1:8000/users/
     ```
   - **Create a User**:
     ```bash
     curl -X POST http://127.0.0.1:8000/users/ \
     -H "Content-Type: application/json" \
     -d '{"username": "johndoe", "email": "john@example.com", "password": "secret", "role": "user"}'
     ```
   - **Delete a User (Admin Only)**:
     ```bash
     curl -X DELETE http://127.0.0.1:8000/users/{id}
     ```

---

## **Future Enhancements**
- Add JWT-based authentication for better security.
- Implement user registration and login.
- Add unit tests for endpoints and models.
- Enhance product features (e.g., categories, filtering).

---

## **License**
This project is licensed under the MIT License. See the `LICENSE` file for details.

---
