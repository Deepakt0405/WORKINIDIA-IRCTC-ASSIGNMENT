# Railway Management System API

A powerful railway management system built using Django, allowing users to register, log in, check seat availability, book tickets, and view booking details. This system supports role-based access control (Admin and User) and ensures secure concurrent seat booking to prevent conflicts.

---

## 🚀 Key Features

- 👥 **User Roles:** Separate functionalities for Admin and User to maintain distinct responsibilities.  
- 🔒 **Secure Booking System:** Prevents double-booking with advanced concurrency handling.  
- 🔑 **Authentication:** Secure user login and registration for a smooth experience.  
- 📖 **API Documentation:** Well-structured endpoints for seamless frontend or system integration.  
- 🗄️ **Database Support:** Uses PostgreSQL for efficient and scalable data storage.  
- ⏱️ **Real-Time Updates:** Instant seat availability updates during booking operations.  
- 🛡️ **Access Control:** Admin APIs are protected with API key authentication.  
- 🚆 **Train Management:** Admins can easily add new trains with source, destination, and seat capacity.  
- 💻 **Cross-Platform Support:** Fully functional on Windows, macOS, and Linux.  
- 📈 **Scalable Architecture:** Designed to handle multiple users and concurrent bookings efficiently.  
- 🔧 **Extensibility:** Modular Django structure for easy feature additions and integrations.  

---

## 🛠️ Installation Guide

1. **Clone the Repository:**
    ```bash
    git clone (https://github.com/Deepakt0405/WORKINIDIA-IRCTC-ASSIGNMENT)
    cd workindia_assignment_railway_management_system
    ```

2. **Set Up a Virtual Environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # For Windows: `venv\Scripts\activate`
    ```

3. **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4. **Install PostgreSQL** if not already installed. Refer to the [PostgreSQL Documentation](https://www.postgresql.org/docs/) for setup instructions.

5. **Configure PostgreSQL Database:**
    ```bash
    psql -U postgres -c "CREATE DATABASE railway_management_test;"
    ```

6. **Update Database Settings:**

    Modify the `DATABASES` section in `settings.py` with your PostgreSQL credentials:
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'railway_management_test',
            'USER': 'your_postgres_username',
            'PASSWORD': 'your_postgres_password',
            'HOST': 'localhost',
            'PORT': '5432',
        }
    }
    ```

---

## 🧑‍💻 Project Setup

1. **Apply Migrations:**
    ```bash
    python manage.py migrate
    ```

2. **Create a Superuser:**
    ```bash
    python manage.py createsuperuser
    ```

3. **Run the Development Server:**
    ```bash
    python manage.py runserver
    ```

---

## 🌐 API Endpoints

Below is a list of available API endpoints, including sample requests and responses.

### 🛂 Authentication Endpoints

1. **User Registration**  
   - **Endpoint:** `/register/`  
   - **Method:** `POST`  
   - **Functionality:** Allows users to sign up with a username, password, and role (Admin/User).  
   - **Request Example:**
     ```json
     {
       "username": "deepak",
       "password": "123456789",
       "is_admin": false
     }
     ```
   - **Response Example:**
     ```json
     {
       "message": "User registered successfully",
       "user_id": 1
     }
     ```

2. **User Login**  
   - **Endpoint:** `/login/`  
   - **Method:** `POST`  
   - **Functionality:** Authenticates users and returns a session token.  
   - **Request Example:**
     ```json
     {
       "username": "deepak",
       "password": "123456789"
     }
     ```
   - **Response Example:**
     ```json
     {
       "message": "Login successful",
       "token": "abcd1234efgh5678"
     }
     ```

---

### 🚆 Train Management Endpoints

1. **Add a Train**  
   - **Endpoint:** `/add_train/`  
   - **Method:** `POST`  
   - **Functionality:** Admins can add new trains by specifying route details and seat capacity.  
   - **Request Example (Admin Only):**
     ```json
     {
       "source": "Bhopal",
       "destination": "Indore",
       "total_seats": 100
     }
     ```
   - **Response Example:**
     ```json
     {
       "message": "Train added successfully",
       "train_id": 10
     }
     ```

2. **Check Seat Availability**  
   - **Endpoint:** `/check_availability/Bhopal/Indore/`  
   - **Method:** `GET`  
   - **Functionality:** Retrieves available seats for a train between specified locations.  
   - **Response Example:**
     ```json
     {
       "source": "Bhopal",
       "destination": "Indore",
       "available_seats": 50
     }
     ```

---

### 🪑 Booking Endpoints

1. **Book a Seat**  
   - **Endpoint:** `/book_seat/`  
   - **Method:** `POST`  
   - **Functionality:** Users can book seats for a specific train.  
   - **Request Example:**
     ```json
     {
       "train_id": 10,
       "seats_to_book": 2
     }
     ```
   - **Response Example:**
     ```json
     {
       "message": "Seats booked successfully",
       "booking_id": 201,
       "booked_seats": 2
     }
     ```

2. **View Booking Details**  
   - **Endpoint:** `/booking_details/`  
   - **Method:** `GET`  
   - **Functionality:** Retrieves all bookings made by the authenticated user.  
   - **Response Example:**
     ```json
     {
       "user_id": 1,
       "bookings": [
         {
           "booking_id": 201,
           "train_id": 10,
           "source": "Bhopal",
           "destination": "Indore",
           "seats_booked": 2,
           "date": "2024-12-01"
         }
       ]
     }
     ```

3. **Authorization Header:**  
   Admin-specific actions require an API key:
   ```bash
   Token: "Token <admin_api_token>"
   ```

