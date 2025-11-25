# 🧮 FastAPI Calculator Application

A modern web-based calculator built with FastAPI, featuring a RESTful API and web interface for performing basic arithmetic operations.

## ✨ Features

- **Basic Operations**: Addition, Subtraction, Multiplication, Division
- **Web Interface**: User-friendly HTML calculator
- **RESTful API**: JSON-based endpoints for programmatic access
- **Comprehensive Testing**: Unit, Integration, and End-to-End tests
- **Docker Support**: Containerized deployment
- **CI/CD Pipeline**: Automated testing and deployment
- **Security Scanning**: Trivy vulnerability scanning

## 🛠️ Technology Stack

- **Backend**: FastAPI (Python 3.10+)
- **Frontend**: HTML, JavaScript
- **Testing**: pytest, Playwright
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Security**: Trivy scanner

---

# 📦 Project Setup

---

# 🧩 1. Install Homebrew (Mac Only)

> Skip this step if you're on Windows.

Homebrew is a package manager for macOS.  
You’ll use it to easily install Git, Python, Docker, etc.

**Install Homebrew:**

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Verify Homebrew:**

```bash
brew --version
```

If you see a version number, you're good to go.

---

# 🧩 2. Install and Configure Git

## Install Git

- **MacOS (using Homebrew)**

```bash
brew install git
```

- **Windows**

Download and install [Git for Windows](https://git-scm.com/download/win).  
Accept the default options during installation.

**Verify Git:**

```bash
git --version
```

---

## Configure Git Globals

Set your name and email so Git tracks your commits properly:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

Confirm the settings:

```bash
git config --list
```

---

## Generate SSH Keys and Connect to GitHub

> Only do this once per machine.

1. Generate a new SSH key:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

(Press Enter at all prompts.)

2. Start the SSH agent:

```bash
eval "$(ssh-agent -s)"
```

3. Add the SSH private key to the agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

4. Copy your SSH public key:

- **Mac/Linux:**

```bash
cat ~/.ssh/id_ed25519.pub | pbcopy
```

- **Windows (Git Bash):**

```bash
cat ~/.ssh/id_ed25519.pub | clip
```

5. Add the key to your GitHub account:
   - Go to [GitHub SSH Settings](https://github.com/settings/keys)
   - Click **New SSH Key**, paste the key, save.

6. Test the connection:

```bash
ssh -T git@github.com
```

You should see a success message.

---

# 🧩 3. Clone the Repository

Now you can safely clone the course project:

```bash
git clone <repository-url>
cd <repository-directory>
```

---

# 🛠️ 4. Install Python 3.10+

## Install Python

- **MacOS (Homebrew)**

```bash
brew install python
```

- **Windows**

Download and install [Python for Windows](https://www.python.org/downloads/).  
✅ Make sure you **check the box** `Add Python to PATH` during setup.

**Verify Python:**

```bash
python3 --version
```
or
```bash
python --version
```

---

## Create and Activate a Virtual Environment

(Optional but recommended)

```bash
python3 -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate.bat  # Windows
```

### Install Required Packages

```bash
pip install -r requirements.txt
```

---

# 🐳 5. Docker Setup


## Install Docker

- [Install Docker Desktop for Mac](https://www.docker.com/products/docker-desktop/)
- [Install Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/)

## Build Docker Image

```bash
docker build -t <image-name> .
```

## Run Docker Container

```bash
docker run -it --rm <image-name>
```

## 🐳 Docker Hub Image The calculator project is published on Docker Hub under: 

- [https://hub.docker.com/r/mihirkadam1912/601_module10/tags](https://hub.docker.com/r/mihirkadam1912/601_module10/tags)

This is the container image that can be pulled and used in any environment that supports Docker.

```bash
docker pull mihirkadam1912/601_module10:latest
```

---

# 🚀 Running the Project

## Development Mode

- **Start the server**:

```bash
python main.py
```

The application will be available at `http://localhost:8000`

- **With virtual environment**:

```bash
source venv/bin/activate  # Mac/Linux
venv\Scripts\activate.bat  # Windows
python main.py
```

## Production Mode (Docker)

```bash
# Build the image
docker build -t calculator-app .

# Run the container
docker run -p 8000:8000 calculator-app
```

## Using Docker Compose

The `docker-compose.yml` file starts three services:

* **web** – the FastAPI calculator app
* **db** – a PostgreSQL database
* **pgadmin** – a browser tool for viewing and managing the database

### ✅ Start All Services

Run this command in the same folder as the `docker-compose.yml` file:

```bash
docker-compose up -d
```

This will:

* build and start the FastAPI app
* start PostgreSQL
* start pgAdmin
* create shared networks and volumes

### ✅ Access the Services

* **FastAPI app:**
  [http://localhost:8000](http://localhost:8000)

* **pgAdmin:**
  [http://localhost:5050](http://localhost:5050)

  * Email: `admin@example.com`
  * Password: `admin`

In pgAdmin, you can add a new server and connect with:

* Host: `db`
* Username: `postgres`
* Password: `postgres`
* Database (default): `fastapi_db`

### ✅ Shut Down Everything

```bash
docker-compose down
```

### ✅ Remove Containers + Volumes

```bash
docker-compose down -v
```

This deletes the PostgreSQL and pgAdmin data volumes.

---

# 🧪 Running Tests Locally

The project has three levels of tests:

* **Unit tests**
* **Integration tests**
* **End-to-end (E2E) tests**
  *(Playwright is needed if you run these)*

Follow the steps below to run everything on your machine.

---

### ✅ 1. Start the Local Database (using docker-compose)

Your tests expect a PostgreSQL test database.
Start the database with:

```bash
docker-compose up -d db
```

The database will run with:

* user: `postgres`
* password: `postgres`
* host: `db`
* db name: `fastapi_test_db` (from your docker-compose environment)

---

### ✅ 2. Set the Test Database URL

Before running tests, set the database URL so tests connect to the right DB:

**Mac/Linux:**

```bash
export DATABASE_URL=postgresql://postgres:postgres@localhost:5432/fastapi_test_db
```

**Windows PowerShell:**

```powershell
setx DATABASE_URL "postgresql://postgres:postgres@localhost:5432/fastapi_test_db"
```

---

### ✅ 3. Create and Activate a Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate          # Mac/Linux
venv\Scripts\activate.bat          # Windows
```

---

### ✅ 4. Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

If you plan to run E2E tests:

```bash
playwright install
```

---

### ✅ 5. Run the Tests

#### Unit tests:

```bash
pytest tests/unit/
```

#### Integration tests:

```bash
pytest tests/integration/
```

#### End-to-end tests:

```bash
pytest tests/e2e/
```

#### Run everything:

```bash
pytest tests/
```

---

### ✅ 6. Optional: Generate Coverage Reports

```bash
pytest tests/ --cov=app --cov-report=term-missing --cov-report=html
```

This creates an HTML coverage report in a folder named `htmlcov/`.

---

### ✅ 7. Stop the Database When Done

```bash
docker-compose down
```

---

# 📚 API Documentation

The application now features secure **User Authentication** and **Authenticated CRUD** operations for calculations. The base URL for the API is `http://localhost:8000`.

## 🔒 User Endpoints (Authentication)

| Method | Endpoint | Description | Request Body | Success Response | Error Codes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **POST** | `/users/register` | Creates a new user account. | `UserCreate` | `201` (`UserRead`) | `400` (User already exists) |
| **POST** | `/users/login` | Authenticates user and issues an **Access Token**. | `{"email": "...", "password": "..."}` | `200` (`{"access_token": "...", "token_type": "bearer"}`) | `401` (Invalid credentials) |
| **GET** | `/users/me` | Fetches the current authenticated user's details. **Requires Access Token.** | None | `200` (`UserRead`) | `401` (Not authenticated) |

### Example API Usage (Authentication)

```bash
# 1. Register a new user
curl -X POST "http://localhost:8000/users/register" \
     -H "Content-Type: application/json" \
     -d '{"username": "testuser", "email": "test@example.com", "password": "securepassword123"}'

# 2. Login to get an access token
# (Assuming the token returned is "YOUR_ACCESS_TOKEN")
curl -X POST "http://localhost:8000/users/login" \
     -H "Content-Type: application/json" \
     -d '{"email": "test@example.com", "password": "securepassword123"}'
```

-----

## 🔢 Calculation Endpoints (CRUD)

All calculation endpoints now require an authenticated user via a **Bearer Token**. They perform the arithmetic operation and persist the result to the database, associated with the user.

| Method | Endpoint | Description | Request Body | Success Response | Error Codes |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **GET** | `/calculations` | **Browse**: Retrieves a list of all calculations by the authenticated user. | None | `200` (List of `CalculationRead`) | `401` |
| **GET** | `/calculations/{id}` | **Read**: Retrieves a specific calculation by ID. | None | `200` (`CalculationRead`) | `401`, `404` |
| **POST** | `/calculations` | **Add (Create)**: Performs an operation (add, subtract, multiply, divide) and saves the result. | `CalculationCreate` | `201` (`CalculationRead`) | `400`, `401` |
| **PATCH** | `/calculations/{id}` | **Edit (Update)**: Modifies an existing calculation record (e.g., updating `a` or `b`). *Re-runs the calculation upon update.* | Partial `CalculationCreate` | `200` (`CalculationRead`) | `401`, `404` |
| **DELETE** | `/calculations/{id}` | **Delete**: Permanently removes a calculation record. | None | `204` (No Content) | `401`, `404` |

### Example API Usage (Calculation)

```bash
# Set your acquired token
TOKEN="YOUR_ACCESS_TOKEN"

# 1. Add (Create) a new calculation (POST /calculations)
curl -X POST "http://localhost:8000/calculations" \
     -H "Authorization: Bearer $TOKEN" \
     -H "Content-Type: application/json" \
     -d '{"type": "add", "a": 20, "b": 5}'

# 2. Browse (List) all calculations (GET /calculations)
curl -X GET "http://localhost:8000/calculations" \
     -H "Authorization: Bearer $TOKEN"

# 3. Read a specific calculation (GET /calculations/{id})
# (Assuming ID 1 exists)
curl -X GET "http://localhost:8000/calculations/1" \
     -H "Authorization: Bearer $TOKEN"
```

-----

# 🐘 SQLAlchemy User Model

The project defines a `User` model using SQLAlchemy.  
It includes the following columns:

- `username`: Must be unique, stores the user's name.  
- `email`: Must be unique, stores the user's email address.  
- `password_hash`: Stores the hashed password securely.  
- `created_at`: Automatically records when the user account was created.  

This ensures that each user is uniquely identifiable and password data is stored safely.

---

# 📝 Pydantic Schemas

Pydantic schemas are used to manage input and output data for the API:

- **UserCreate**: Used when registering a new user, includes `username`, `email`, and `password`.  
- **UserRead**: Used when returning user details, includes `id`, `username`, `email`, and `created_at` but does **not** include the password hash.  
- **CalculationCreate**: Used when creating a new calculation, includes `type`, `a`, `b`, and `user_id`. 
- **CalculationRead**: Used when returning a calculation result, includes `id`, `type`, `a`, `b`, `user_id`, `result`, `created_at`, and `updated_at`. These schemas ensure proper data validation and enforce business rules like no division by zero.

These schemas ensure proper data validation and security by not exposing sensitive information.

---

# 🔒 Password Hashing

Passwords are stored securely by hashing before saving to the database.  

- A hashing function converts plain-text passwords into a secure hash.  
- A verification function checks if a plain-text password matches the stored hash.  

This approach keeps user passwords safe and ensures authentication works securely.

---

# 🧪 Testing

## Test Types

### Unit Tests
Test individual functions in isolation:
```bash
pytest tests/unit/ --cov=app --cov-report=html
```

### Integration Tests
Test API endpoints with TestClient:
```bash
pytest tests/integration/ --cov=app --cov-append
```

### End-to-End Tests
Test complete user workflows with Playwright:
```bash
pytest tests/e2e/ --cov=app --cov-append
```

## Running All Tests

```bash
# Run all tests with coverage
pytest tests/ --cov=app --cov-report=html --cov-report=term-missing

# Run specific test categories
pytest -m "not e2e"  # Skip E2E tests
pytest -m "e2e"       # Only E2E tests
```

## Coverage Requirements

- **Unit Tests**: 100% coverage required
- **Integration Tests**: API endpoint coverage
- **E2E Tests**: User workflow validation

---

# 🏗️ Project Structure

```
module8_is601/
├── app/
│   └── operations/          # Calculator functions
│       └── __init__.py
├── tests/
│   ├── unit/               # Unit tests
│   ├── integration/        # API integration tests
│   ├── e2e/               # End-to-end tests
│   └── conftest.py        # Test fixtures
├── templates/
│   └── index.html         # Web interface
├── .github/workflows/     # CI/CD pipeline
├── main.py               # FastAPI application
├── Dockerfile           # Container configuration
├── docker-compose.yml   # Multi-container setup
├── requirements.txt     # Python dependencies
└── pytest.ini         # Test configuration
```

---

# 🔄 CI/CD Pipeline

## GitHub Actions Workflow

The project uses GitHub Actions for automated testing and deployment:

### Test Job
- **Python Setup**: Python 3.10
- **Dependencies**: Install requirements and Playwright
- **Test Execution**: Unit, Integration, and E2E tests
- **Coverage**: Generate coverage reports

### Security Job
- **Docker Build**: Build application image
- **Trivy Scan**: Vulnerability scanning
- **Severity**: CRITICAL and HIGH vulnerabilities block deployment

### Deploy Job
- **Docker Hub**: Push to registry
- **Multi-platform**: linux/amd64, linux/arm64
- **Tags**: latest and commit SHA

## Manual Deployment

```bash
# Build and push to Docker Hub
docker build -t yourusername/calculator-app .
docker push yourusername/calculator-app
```

---

# 🛡️ Security

## Vulnerability Scanning

The project uses Trivy for security scanning:

- **Automated**: Runs on every CI/CD pipeline
- **Severity Levels**: CRITICAL and HIGH vulnerabilities block deployment
- **Ignored CVEs**: Listed in `.trivyignore`

## Security Best Practices

- **Non-root User**: Application runs as `appuser`
- **Minimal Image**: Uses Python slim base image
- **Dependency Updates**: Regular security updates
- **Input Validation**: Pydantic models validate all inputs

---

# 🐛 Troubleshooting

## Common Issues

### Port Already in Use
```bash
# Kill process using port 8000
lsof -ti:8000 | xargs kill -9
```

### Docker Build Fails
```bash
# Clean Docker cache
docker system prune -a
```

### Tests Fail
```bash
# Install Playwright browsers
playwright install
```

### Permission Denied
```bash
# Fix file permissions
chmod +x scripts/*
```

## Error Messages

| Error | Solution |
|-------|----------|
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| `Port 8000 already in use` | Kill existing process or use different port |
| `Docker permission denied` | Add user to docker group or use sudo |

---

---


# 📋 Notes

- Install **Homebrew** first on Mac.
- Install and configure **Git** and **SSH** before cloning.
- Use **Python 3.10+** and **virtual environments** for Python projects.
- Install **Docker** to run this project.

---

# 📎 Quick Links

- [Homebrew](https://brew.sh/)
- [Git Downloads](https://git-scm.com/downloads)
- [Python Downloads](https://www.python.org/downloads/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [GitHub SSH Setup Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)