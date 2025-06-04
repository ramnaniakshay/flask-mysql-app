# Flask MySQL Connection Application

A simple Flask application that connects to a MySQL database and displays all available databases on a clean, user-friendly interface.

## Project Overview

This application demonstrates how to:
- Connect a Flask application to a MySQL database
- Store database credentials securely in a separate configuration file
- Display connection status and database information
- Handle connection errors gracefully

## Project Structure

```
flask_mysql_app/
├── app.py              # Main Flask application
├── config.py           # Database configuration settings (separate file)
├── requirements.txt    # Project dependencies
├── venv/               # Virtual environment
└── templates/
    └── home.html       # Home page template
```

## Prerequisites

- Python 3.x
- MySQL Server
- pip (Python package manager)

## Installation

1. Clone this repository or download the source code:
   ```
   git clone <repository-url>
   cd flask_mysql_app
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
   CREATE USER 'flaskuser'@'localhost' IDENTIFIED BY 'flaskpass';
   GRANT ALL PRIVILEGES ON *.* TO 'flaskuser'@'localhost';
   FLUSH PRIVILEGES;
   ```

## Running the Application

1. Start the Flask application:
   ```
   python app.py
   ```

2. Access the application:
   - Open your browser and navigate to `http://127.0.0.1:5000/`
   - The page will display connection status and list all available databases

## Features

- **Clean UI**: Simple and responsive interface showing connection status
- **Database Listing**: Displays all databases available to the connected user
- **Error Handling**: Gracefully handles and displays database connection errors
- **Separate Configuration**: Keeps database credentials in a separate file for security

## Security Considerations

- The configuration file (`config.py`) contains sensitive database credentials and should not be committed to version control
- Consider using environment variables for production deployments
- Restrict database user permissions to only what is necessary for the application

## Troubleshooting

- **Connection Error**: Verify MySQL credentials and ensure MySQL server is running
- **Access Denied**: Check that the user has appropriate permissions
- **Import Error**: Ensure all dependencies are installed via `pip install -r requirements.txt`

## License

MIT License

## Acknowledgments

- Flask - Python web framework
- MySQL Connector - Python driver for MySQL