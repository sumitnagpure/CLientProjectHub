# ClientProjectHub - Django Project for Client and Project Management

**ClientProjectHub** is a Django-based application designed to manage clients, projects, and users. It provides RESTful APIs to create, read, update, and delete clients and projects and assign users to these projects. The application utilizes Django and Django REST Framework (DRF) to handle API requests and includes JWT authentication for secure access.

## Features
- Register and manage clients
- CRUD operations for client data
- Create and manage projects for clients
- Assign users to specific projects
- Retrieve information about projects assigned to users

## Technologies Used
- Python 3.x
- Django 4.x
- Django REST Framework (DRF)
- PostgreSQL (or MySQL)
- JWT Authentication

## Installation

### Prerequisites
- Python 3.x installed
- PostgreSQL (or MySQL) database set up
- Virtual environment tool (recommended)

### 1. Clone the repository:
```bash
git clone https://github.com/yourusername/ClientProjectHub.git
cd ClientProjectHub
```

### 2. Set up a virtual environment:
For Windows:
```bash
python -m venv venv
.\venv\Scripts\activate
```
For macOS/Linux:
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies:
```bash
pip install -r requirements.txt
```

### 4. Set up the database:
1. Configure your database settings in `settings.py`.
2. Run the migrations:
```bash
python manage.py migrate
```

### 5. Create a superuser (to access the admin panel):
```bash
python manage.py createsuperuser
```

### 6. Start the development server:
```bash
python manage.py runserver
```

Your API will be available at `http://127.0.0.1:8000/`.

## API Endpoints

### 1. **Client Management**

- **Get all clients:**
```bash
GET /clients/
```
**Response:**
```json
[
  {
    "id": 1,
    "client_name": "Nimap",
    "created_at": "2024-12-18T11:03:55",
    "created_by": "Rohit"
  }
]
```

- **Create a new client:**
```bash
POST /clients/
```
**Input:**
```json
{
  "client_name": "Company A"
}
```

**Response:**
```json
{
  "id": 2,
  "client_name": "Company A",
  "created_at": "2024-12-18T11:03:55",
  "created_by": "Rohit"
}
```

- **Get client details by ID:**
```bash
GET /clients/<id>/
```
**Response:**
```json
{
  "id": 2,
  "client_name": "Company A",
  "created_at": "2024-12-18T11:03:55",
  "projects": [
    {
      "id": 1,
      "name": "Project A"
    }
  ],
  "created_by": "Rohit"
}
```

- **Update client details:**
```bash
PUT /clients/<id>/
```
**Input:**
```json
{
  "client_name": "Updated Company A"
}
```

- **Delete client:**
```bash
DELETE /clients/<id>/
```

### 2. **Project Management**

- **Create a new project for a client:**
```bash
POST /clients/<id>/projects/
```
**Input:**
```json
{
  "project_name": "Project A",
  "users": [
    {
      "id": 1,
      "username": "sumit"
    }
  ]
}
```

**Response:**
```json
{
  "id": 1,
  "project_name": "Project A",
  "client": "Company A",
  "users": [
    {
      "id": 1,
      "username": "sumit"
    }
  ],
  "created_at": "2024-12-18T11:03:55",
  "created_by": "Ganesh"
}
```

- **Get all projects assigned to the logged-in user:**
```bash
GET /projects/
```
**Response:**
```json
[
  {
    "id": 1,
    "project_name": "Project A",
    "created_at": "2024-12-18T11:03:55",
    "created_by": "Ganesh"
  }
]
```

## Authentication

- **JWT Authentication** is used for securing API endpoints.
- Obtain a token by sending a POST request to `http://127.0.0.1:8000/token/` with your credentials:

**Input:**
```json
{
  "username": "yourusername",
  "password": "yourpassword"
}
```

**Response:**
```json
{
  "access": "your_jwt_access_token",
  "refresh": "your_jwt_refresh_token"
}
```

Use the `access` token for API requests in the `Authorization` header:
```bash
Authorization: Bearer <your_access_token>
```

## License
This project is licensed under the MIT License.

## Acknowledgments
- Django framework
- Django REST Framework (DRF)
