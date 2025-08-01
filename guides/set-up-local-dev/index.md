# Set up local development environment

1. Install the following software:

- Windows Terminal
- VS Code
- Visual Studio Community (for desktop development)
- Bruno Client
- Navicat (or any other postgreSQL GUI)

2. Install the following inside of Windows Terminal:

- Ubuntu
- PostgreSQL
- Redis
- Git
- Github CLI
- NodeJS
- Python3

3. Create databases and assign a password to postgresql
```
# Create database
CREATE DATABASE "mydatabase";

# Assign password
ALTER USER postgres PASSWORD 'postgres';

# Remove database
DROP DATABASE "mydatabase";
```

