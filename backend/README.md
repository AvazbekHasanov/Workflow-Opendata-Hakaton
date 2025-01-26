# WorkFlow: Project Management Platform  

WorkFlow is a comprehensive project management platform designed to simplify the management of project documentation, tasks, and employees. Built using Java and Spring Boot, this backend solution provides robust support for real-time updates, email notifications, and secure data handling.

## Features  

- Task Management: Assign, track, and manage tasks efficiently.  
- Employee Management: Maintain a centralized database for employee records.  
- Project Documentation: Store and manage project-related documents securely.  
- Real-Time Updates: Keep users informed using WebSocket for real-time notifications.  
- Email Notifications: Integrated email service to notify users about important updates.  
- Secure Access: Role-based authentication and authorization using Spring Security and JWT.  

---

## Tech Stack  

- Programming Language: Java 21  
- Framework: Spring Boot 3.4.1  
- Database: PostgreSQL  
- Real-Time Communication: WebSocket  
- Security: Spring Security, JWT Authentication  
- Documentation: SpringDoc OpenAPI  
- Other Libraries: 
  - Lombok for reducing boilerplate code  
  - MapStruct for object mapping  
  - iText for PDF generation  
  - JJWT for token management  

---

## Prerequisites  

1. Java 21 installed on your system.  
2. PostgreSQL database with the required credentials.  
3. Maven Central Repository access for dependencies.  

---

## Installation  

1. Clone the repository:  
   
   git clone https://github.com/your-username/workflow-backend.git
   cd workflow-backend
   

2. Configure application properties:  
   Update the application.yml or application.properties file with your database and email service credentials.  

3. Build the project:  
   
   ./gradlew build
   

4. Run the application:  
   
   ./gradlew bootRun
   

---

## Endpoints  

The API documentation is available via OpenAPI at:  
http://localhost:8080/swagger-ui/index.html  

### Sample Endpoints  

- User Management:  
  - POST /users/register - Register a new user.  
  - GET /users - Get all users.  

- Task Management:  
  - POST /tasks - Create a new task.  
  - GET /tasks/{id} - Get task details.  

- Project Documentation:  
  - POST /documents - Upload project documents.  
  - GET /documents/{id} - Fetch document details.  

---

## Development  

### Dependencies  

This project uses the following dependencies:  

- Spring Boot Modules: Web, Data JPA, WebSocket, Security, Mail  
- Database: PostgreSQL Driver  
- OpenAPI: SpringDoc OpenAPI Starter  
- PDF Support: iText  

### Build Tool  

The project uses Gradle for dependency management and building.  

---

## Contributing  

We welcome contributions! Please follow these steps:  

1. Fork the repository.  
2. Create a new feature branch:  
   
   git checkout -b feature/your-feature-name
   
  
3. Commit your changes and open a pull request.  

---

## License  

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.  
