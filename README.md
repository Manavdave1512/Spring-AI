# Spring AI Application Setup

## 🛠️ Tech Stack
- **Backend:** Spring Boot (Java)
- **Frontend:** HTML, CSS, JavaScript
- **Database:** MySQL

## 🚀 Getting Started

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/Manavdave1512/Spring-AI.git
cd Spring-AI
```

### 2️⃣ Configure Your Database
Navigate to `src/main/resources/application.properties` and update with your database details:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/your_db_name
spring.datasource.username=your_db_username
spring.datasource.password=your_db_password

# JPA/Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
```

**Note:** Make sure to:
- Create the database `your_db_name` in MySQL before running the application
- Replace `your_db_name`, `your_db_username`, and `your_db_password` with your actual database credentials
- Ensure MySQL server is running on your local machine

### 3️⃣ Prerequisites
Make sure you have the following installed:
- **Java 17 or higher** - [Download here](https://adoptium.net/)
- **Maven 3.6+** - [Download here](https://maven.apache.org/download.cgi) (or use the included Maven wrapper)
- **MySQL 8.0+** - [Download here](https://dev.mysql.com/downloads/mysql/)

**Verify installations:**
```bash
java -version
mvn -version  # or use ./mvnw -version
mysql --version
```

### 4️⃣ Run the Spring Boot Backend
Navigate to the project directory and run:

```bash
# Using Maven wrapper (recommended - no Maven installation required)
./mvnw spring-boot:run          # Unix/Linux/Mac
mvnw.cmd spring-boot:run        # Windows

# Or using installed Maven
mvn spring-boot:run
```

**Successful startup indicators:**
- Console shows: `Started [ApplicationName] in X.XXX seconds`
- No error messages in the logs
- Application runs on `http://localhost:8080`


### 5️⃣ Run the HTML/CSS/JS Frontend
Since this is a static frontend, you have several options:

**Option 1: Simple Browser Opening (Quick Start)**
```bash
# Navigate to the frontend directory (if separate) or project root
# Open index.html directly in browser
open index.html       # Mac
start index.html      # Windows
xdg-open index.html   # Linux
```
**Option 2: VS Code Live Server Extension**
1. Install "Live Server" extension in VS Code
2. Right-click on `index.html`
3. Select "Open with Live Server"
4. Automatically opens at `http://127.0.0.1:5500`

## 🔧 Troubleshooting

### Common Issues:

**1. Database Connection Error:**
```bash
# Check if MySQL is running
sudo service mysql status        # Linux
brew services list | grep mysql # Mac
net start mysql                 # Windows (as Admin)

# Test database connection
mysql -u your_db_username -p -h localhost -P 3306
```
- Verify database credentials in `application.properties`
- Ensure the database exists: `CREATE DATABASE your_db_name;`
- Check if MySQL is running on port 3306

**2. Spring Boot Port Already in Use (8080):**
```bash
# Find process using port 8080
lsof -ti:8080           # Mac/Linux
netstat -ano | findstr :8080  # Windows

# Kill the process
kill -9 <PID>           # Mac/Linux
taskkill /PID <PID> /F  # Windows

# Or change port in application.properties
server.port=8081
```

**3. Maven/Build Issues:**
```bash
# Clean and rebuild
./mvnw clean install

# Skip tests if they're failing
./mvnw spring-boot:run -Dmaven.test.skip=true

# Update dependencies
./mvnw dependency:resolve
```

**4. Frontend-Backend Communication (CORS):**
- Ensure backend is running on `http://localhost:8080`
- Frontend should be served via HTTP server (not file://)
- Check browser console for CORS errors
- Add CORS configuration in Spring Boot if needed:
```java
@CrossOrigin(origins = "http://localhost:3000")
```

**5. JavaScript/API Call Issues:**
- Open browser Developer Tools (F12)
- Check Console tab for JavaScript errors
- Check Network tab for failed API requests
- Verify API endpoints are correct in your JS files

## 📸 Screenshots

### 🗨️ General Chat
![General Chat](screenshots/general_chat.png)

### 🛍️ E-commerce Product Search
![E-commerce Search](screenshots/ecommerce_search.png)

## 📝 Project Structure & Notes

```
Spring-AI/
├── Genie-AI/
|   ├── src/main/
│   │   ├── java/           # Spring Boot application code
│   │   └── resources/
│   │       └── application.properties
├── UI/               # HTML, CSS, JS files (if in separate folder)
│   ├── index.html
│   ├── style.css
│   └── script.js
├── pom.xml                # Maven dependencies
└── mvnw                   # Maven wrapper
```

**Important Notes:**
- **Backend runs on:** `http://localhost:8080`
- **Frontend runs on:** `http://localhost:3000` (or chosen port)
- **Database:** MySQL on `localhost:3306`
- Both frontend and backend must be running simultaneously
- Frontend makes AJAX/Fetch API calls to Spring Boot REST endpoints
- Check browser console and Spring Boot logs for debugging
- Default Spring Boot API base path: `http://localhost:8080/api/`