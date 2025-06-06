# Flask MySQL Connection Application

A simple Flask application that connects to a MySQL database and displays all available databases on a clean, user-friendly interface.

## Project Overview

This application demonstrates how to:
- Connect a Flask application to a MySQL database
- Store database credentials securely in a separate configuration file or environment variables
- Display connection status and database information
- Handle connection errors gracefully
- Run the application in a Docker container

## Project Structure

```
flask-mysql-app/
├── app.py              # Main Flask application (for local development)
├── app_docker.py       # Docker-ready version of the Flask application
├── config.py           # Database configuration settings (for local development)
├── Dockerfile          # Docker configuration for containerization
├── requirements.txt    # Project dependencies
└── templates/
    └── home.html       # Home page template
```

## Prerequisites

- Python 3.x
- MySQL Server
- pip (Python package manager)
- Docker (for containerized deployment)

## Installation

1. Clone this repository or download the source code:
   ```
   git clone https://github.com/yourusername/flask-mysql-app.git
   cd flask-mysql-app
   ```

2. Create and activate a virtual environment:
   ```
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install the required dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Configure your MySQL connection:
   - Option 1: Using config.py (for local development)
     - Open `config.py` and update the MySQL credentials with your own:
     ```python
     MYSQL_CONFIG = {
         'host': 'localhost',
         'user': 'your_username',
         'password': 'your_password',
         'port': 3306
     }
     ```

## Database Setup

1. Ensure your MySQL server is running
2. Create a user with appropriate permissions:
   ```sql
   CREATE USER 'flaskuser'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON *.* TO 'flaskuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

## Running the Application

### Local Development

1. Start the Flask application:
   ```
   python app.py
   ```

2. Access the application:
   - Open your browser and navigate to `http://127.0.0.1:5000/`
   - The page will display connection status and list all available databases

### Docker Deployment

1. Build the Docker image:
   ```
   docker build -t flask-mysql-app .
   ```

2. Run the Docker container:
   ```
   docker run -p 5000:5000 \
     -e MYSQL_HOST=your_mysql_host \
     -e MYSQL_USER=your_username \
     -e MYSQL_PASSWORD=your_password \
     -e MYSQL_PORT=3306 \
     flask-mysql-app
   ```

   Note: Replace `your_mysql_host`, `your_username`, and `your_password` with your actual MySQL credentials.

3. If your MySQL server is running on the host machine, you'll need to use the host's IP address instead of 'localhost':
   
   For Linux:
   ```
   docker run -p 5000:5000 \
     -e MYSQL_HOST=172.17.0.1 \
     -e MYSQL_USER=your_username \
     -e MYSQL_PASSWORD=your_password \
     -e MYSQL_PORT=3306 \
     flask-mysql-app
   ```

   For macOS and Windows:
   ```
   docker run -p 5000:5000 \
     -e MYSQL_HOST=host.docker.internal \
     -e MYSQL_USER=your_username \
     -e MYSQL_PASSWORD=your_password \
     -e MYSQL_PORT=3306 \
     flask-mysql-app
   ```

4. Using Docker Compose (optional):
   
   Create a `docker-compose.yml` file:
   ```yaml
   version: '3'
   services:
     web:
       build: .
       ports:
         - "5000:5000"
       environment:
         - MYSQL_HOST=mysql
         - MYSQL_USER=flaskuser
         - MYSQL_PASSWORD=your_password
         - MYSQL_PORT=3306
       depends_on:
         - mysql
     
     mysql:
       image: mysql:8.0
       environment:
         - MYSQL_ROOT_PASSWORD=rootpassword
         - MYSQL_DATABASE=flaskapp
         - MYSQL_USER=flaskuser
         - MYSQL_PASSWORD=your_password
       ports:
         - "3306:3306"
       volumes:
         - mysql_data:/var/lib/mysql

   volumes:
     mysql_data:
   ```

   Then run:
   ```
   docker-compose up
   ```

5. Access the application:
   - Open your browser and navigate to `http://localhost:5000/`

## Features

- **Clean UI**: Simple and responsive interface showing connection status
- **Database Listing**: Displays all databases available to the connected user
- **Error Handling**: Gracefully handles and displays database connection errors
- **Separate Configuration**: Keeps database credentials in a separate file for security

## Security Considerations

- The configuration file (`config.py`) contains sensitive database credentials and should not be committed to version control
- Consider using environment variables for production deployments
- Restrict database user permissions to only what is necessary for the application
- Never use default or weak passwords in production environments
- Consider using Docker secrets or a secure vault for managing credentials in production

## Troubleshooting

- **Connection Error**: Verify MySQL credentials and ensure MySQL server is running
- **Access Denied**: Check that the user has appropriate permissions
- **Import Error**: Ensure all dependencies are installed via `pip install -r requirements.txt`
- **Docker Connection Issues**: If connecting to a MySQL server on your host machine, make sure to use `host.docker.internal` instead of `localhost`

## License

MIT License