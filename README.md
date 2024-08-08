# Dockerized-Flask-with-MySQL-Integration
"A simple Flask app containerized with Docker, integrating MySQL for backend data storage, allowing users to submit and view messages."


# Dockerized Flask with MySQL Integration

This project demonstrates a simple Flask application integrated with a MySQL database, containerized using Docker. The app allows users to submit messages, which are then stored in the database and displayed on the frontend.

## Prerequisites

Before getting started, ensure you have the following tools installed on your machine:

- Docker
- Git (optional, for cloning the repository)

## Setup

### 1. Clone the Repository

First, clone this repository to your local machine:

```bash
git clone https://github.com/your-username/your-repo-name.git
```

### 2. Navigate to the Project Directory

Move into the project directory by running:

```bash
cd your-repo-name
```

### 3. Create a `.env`  File

Inside the project directory, create a `.env` file to store your MySQL environment variables:

``` bash
touch .env
```

### 4. Configure MySQL Settings

Open the `.env` file and configure your MySQL settings as follows:

```env
MYSQL_HOST=mysql
MYSQL_USER=your_username
MYSQL_PASSWORD=your_password
MYSQL_DB=your_database
```

## Usage

### 1. Build and Start the Docker Containers

Use Docker Compose to build and start the containers:

``` bash
docker-compose up --build
```

### 2. Access the Flask App

Once the containers are running, you can access the app through your web browser:

- **Frontend:** [http://localhost](http://localhost)
- **Backend:** [http://localhost:5000](http://localhost:5000)

### 3. Set Up the MySQL Database

To create the `messages` table in your MySQL database, use a MySQL client or a tool like phpMyAdmin to run the following SQL:

```sql
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT
);

```

### 4. Interact with the Application

- Visit [http://localhost](http://localhost) to view the frontend and submit messages.
- Visit [http://localhost:5000/insert_sql](http://localhost:5000/insert_sql) to directly insert a message into the database via an SQL query.

## Cleaning Up

To stop and remove the Docker containers, press Ctrl+C in the terminal where the containers are running, or run:

```bash
docker-compose down
```

## Running Without Docker Compose

### 1. Build the Docker image from the Dockerfile
``` bash
docker build -t flaskapp .
```
### 2. Create a Docker network:
``` bash
docker network create twotier
```

### 3. Run the MySQL container:
```bash
docker run -d \
    --name mysql \
    -v mysql-data:/var/lib/mysql \
    --network=twotier \
    -e MYSQL_DATABASE=mydb \
    -e MYSQL_USER=root \
    -e MYSQL_ROOT_PASSWORD=admin \
    -p 3306:3306 \
    mysql:5.7

```
### 4. Run the Flask app container:
``` bash
docker run -d \
    --name flaskapp \
    --network=twotier \
    -e MYSQL_HOST=mysql \
    -e MYSQL_USER=root \
    -e MYSQL_PASSWORD=admin \
    -e MYSQL_DB=mydb \
    -p 5000:5000 \
    flaskapp:latest

```

## Notes

- Be sure to replace placeholders (like `your_username`, `your_password`, `your_database`) with your actual MySQL credentials.
- This setup is for basic demonstration purposes. For production environments, adhere to best practices for security and performance.
- Be cautious when executing SQL queries directly. Ensure that user inputs are validated and sanitized to prevent SQL injection vulnerabilities.
- If you encounter any issues, check the Docker logs and error messages for troubleshooting.
  
