# JWT Authentication Spring Boot Application

A secure REST API application built with Spring Boot that implements JWT (JSON Web Token) authentication for user registration and login functionality.

## 🚀 Features

- **User Registration & Login**: Complete authentication system with email/password
- **JWT Token Management**: Secure token generation, validation, and expiration handling
- **Password Security**: BCrypt password encoding for secure password storage
- **Database Integration**: PostgreSQL database with JPA/Hibernate for data persistence
- **RESTful API**: Clean REST endpoints for authentication operations
- **Security Configuration**: Spring Security with JWT filter implementation
- **Protected Endpoints**: Demo endpoint requiring authentication

## 🛠️ Tech Stack

- **Java 21**
- **Spring Boot 3.5.5**
- **Spring Security**
- **Spring Data JPA**
- **PostgreSQL Database**
- **JWT (JSON Web Tokens)**
- **Lombok** (for reducing boilerplate code)
- **Maven** (dependency management)

## 📋 Prerequisites

Before running this application, make sure you have:

- Java 21 or higher
- Maven 3.6+
- PostgreSQL database
- IDE (IntelliJ IDEA, Eclipse, or VS Code)

## 🗄️ Database Setup

1. Install PostgreSQL on your system
2. Create a database named `jwt_security`:
   ```sql
   CREATE DATABASE jwt_security;
   ```
3. Update the database credentials in `src/main/resources/application.properties` if needed

## ⚙️ Configuration

The application uses the following configuration in `application.properties`:

```properties
spring.application.name=demo
server.port=8080
spring.datasource.url=jdbc:postgresql://localhost:5432/jwt_security
spring.datasource.username=postgres
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRATION_MS=3600000
```

**Important**: Change the `JWT_SECRET` to a secure random string in production!

## 🚀 Getting Started

1. **Clone the repository**:

   ```bash
   git clone <repository-url>
   cd JwtTutorial
   ```

2. **Update database credentials** in `src/main/resources/application.properties`

3. **Build the application**:

   ```bash
   mvn clean install
   ```

4. **Run the application**:

   ```bash
   mvn spring-boot:run
   ```

   Or run the JAR file:

   ```bash
   java -jar target/demo-0.0.1-SNAPSHOT.jar
   ```

The application will start on `http://localhost:8080`

## 📚 API Endpoints

### Authentication Endpoints

#### Register User

- **POST** `/api/auth/register`
- **Request Body**:
  ```json
  {
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com"
  }
  ```

#### Login User

- **POST** `/api/auth/login`
- **Request Body**:
  ```json
  {
    "email": "john.doe@example.com",
    "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com"
  }
  ```

### Protected Endpoints

#### Demo Endpoint

- **GET** `/api/demo/hello`
- **Headers**: `Authorization: Bearer <your-jwt-token>`
- **Response**: `"Hello world"`

## 🔐 Security Features

- **JWT Authentication**: Stateless authentication using JSON Web Tokens
- **Password Encryption**: BCrypt hashing for secure password storage
- **Token Expiration**: Configurable token expiration (default: 1 hour)
- **Protected Routes**: All endpoints except `/api/auth/**` require authentication
- **CORS Configuration**: Cross-origin resource sharing support

## 📁 Project Structure

```
src/
├── main/
│   ├── java/com/example/demo/
│   │   ├── Config/
│   │   │   ├── JwtAuthenticationEntryPoint.java
│   │   │   └── SecurityConfig.java
│   │   ├── Controller/
│   │   │   ├── AuthController.java
│   │   │   └── DemoController.java
│   │   ├── DTO/
│   │   │   ├── AuthResponse.java
│   │   │   ├── LoginRequest.java
│   │   │   └── RegisterRequest.java
│   │   ├── Entity/
│   │   │   ├── Role.java
│   │   │   └── User.java
│   │   ├── Repository/
│   │   │   └── UserRepository.java
│   │   ├── Service/
│   │   │   ├── CustomUserDetailsService.java
│   │   │   └── UserService.java
│   │   ├── Util/
│   │   │   ├── JwtAuthenticationFilter.java
│   │   │   └── JwtUtil.java
│   │   └── DemoApplication.java
│   └── resources/
│       └── application.properties
└── test/
    └── java/com/example/demo/
        └── DemoApplicationTests.java
```

## 🧪 Testing the API

### Using cURL

1. **Register a new user**:

   ```bash
   curl -X POST http://localhost:8080/api/auth/register \
     -H "Content-Type: application/json" \
     -d '{
       "firstName": "John",
       "lastName": "Doe",
       "email": "john.doe@example.com",
       "password": "password123"
     }'
   ```

2. **Login**:

   ```bash
   curl -X POST http://localhost:8080/api/auth/login \
     -H "Content-Type: application/json" \
     -d '{
       "email": "john.doe@example.com",
       "password": "password123"
     }'
   ```

3. **Access protected endpoint**:
   ```bash
   curl -X GET http://localhost:8080/api/demo/hello \
     -H "Authorization: Bearer YOUR_JWT_TOKEN"
   ```

### Using Postman

1. Import the collection or create requests manually
2. Set the base URL to `http://localhost:8080`
3. For protected endpoints, add the JWT token in the Authorization header as `Bearer <token>`

## 🔧 Development

### Running Tests

```bash
mvn test
```

### Building for Production

```bash
mvn clean package -Pproduction
```

## 🚨 Security Considerations

- **Change JWT Secret**: Always use a strong, random JWT secret in production
- **HTTPS**: Use HTTPS in production to protect tokens in transit
- **Token Storage**: Store JWT tokens securely on the client side
- **Password Policy**: Implement strong password requirements
- **Rate Limiting**: Consider implementing rate limiting for auth endpoints

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Troubleshooting

### Common Issues

1. **Database Connection Error**: Ensure PostgreSQL is running and credentials are correct
2. **JWT Token Invalid**: Check if the token has expired or the secret key is correct
3. **Port Already in Use**: Change the port in `application.properties` or stop the conflicting service

### Logs

Check the console output for detailed error messages and stack traces.

## 📞 Support

If you encounter any issues or have questions, please open an issue in the repository.

---

**Happy Coding! 🎉**
