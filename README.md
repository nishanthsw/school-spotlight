# school-spotlight
School Spotlight evaluates and ranks educational institutions based on factors such as academic performance, teacher quality, facilities, student satisfaction, and extracurricular offerings.
# **Software Design Document for School Rating Website**

## **1. Introduction**

### **1.1 Purpose**
The purpose of this Software Design Document (SDD) is to provide a detailed description of the design for the School Rating Website. This website allows users to rate and review schools, providing valuable feedback to prospective students and parents. The platform will include features such as school ratings, user reviews, search and filter options, and a user-friendly interface.

### **1.2 Scope**
The School Rating Website will allow users to:
- Search for schools based on location, type, and rating.
- Read reviews and ratings provided by other users.
- Rate schools based on various criteria (e.g., facilities, teaching quality, extracurricular activities).
- Allow school administrators to manage reviews and ratings.
- Provide a responsive, accessible interface that works across devices.

### **1.3 Definitions, Acronyms, and Abbreviations**
- **User:** Any person who visits the website and interacts with the system.
- **Admin:** A user with elevated privileges responsible for managing school data, reviews, and user interactions.
- **Rating:** A numerical score provided by a user to rate a school.
- **Review:** A written comment accompanying a rating.

### **1.4 References**
- [W3C Web Content Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [MySQL Documentation](https://dev.mysql.com/doc/)

---

## **2. System Overview**

### **2.1 High-Level System Architecture**
The system will follow a **client-server architecture** with the following components:

- **Frontend (Client-side)**: A web application built using **HTML, CSS, JavaScript**, and **React** (for dynamic content rendering).
- **Backend (Server-side)**: A REST API built using **Node.js** and **Express.js**.
- **Database**: A relational database, specifically **MySQL**, for storing user and school data, ratings, reviews, etc.
- **Authentication**: User authentication will be handled through **JWT (JSON Web Tokens)** for secure access.

### **2.2 System Components**
1. **Frontend (Web Interface):**
   - Displays school ratings, reviews, and allows for searching/filtering.
   - Handles user input for submitting ratings and reviews.
   
2. **Backend (API Layer):**
   - Handles user registration, authentication, and data submission.
   - Processes requests from the frontend and interacts with the database.
   - Validates and sanitizes user input to prevent malicious content.
   
3. **Database:**
   - Stores user data, school information, reviews, and ratings.
   - Ensures data consistency and integrity.
   
4. **Admin Dashboard (Admin Panel):**
   - Provides functionality for school administrators to manage content, including reviewing and removing inappropriate reviews.

---

## **3. Functional Requirements**

### **3.1 User Registration and Authentication**
- **Requirement 1**: Users must be able to register by providing an email, username, and password.
- **Requirement 2**: After registration, users must be able to log in using their credentials (username/email and password).
- **Requirement 3**: Implement **JWT-based authentication** to manage user sessions.

### **3.2 School Rating and Review System**
- **Requirement 4**: Users must be able to search for schools by name, location, or rating.
- **Requirement 5**: Users can submit a rating (1 to 5 stars) for a school based on different criteria (e.g., teaching, facilities).
- **Requirement 6**: Users can write a review and link it to their rating.
- **Requirement 7**: Users can view aggregated ratings for each school.
- **Requirement 8**: Users can filter reviews based on rating score, date, or helpfulness.

### **3.3 Admin Features**
- **Requirement 9**: Admins should be able to manage school data (e.g., add/edit schools, view reviews).
- **Requirement 10**: Admins can approve or reject reviews that violate terms of service.
- **Requirement 11**: Admins can view aggregated statistics (e.g., average rating, number of reviews).

---

## **4. Non-Functional Requirements**

### **4.1 Usability**
- The website should be easy to navigate, with intuitive design and clear labels.
- It should be responsive and adapt to different screen sizes (desktop, tablet, mobile).

### **4.2 Performance**
- The website should load within 3 seconds on average.
- The server should be able to handle up to 500 concurrent users without significant degradation in performance.

### **4.3 Security**
- All user passwords must be stored securely using encryption algorithms like **bcrypt**.
- **SQL injection** and **XSS** protections should be in place for all user input.
- The website should use HTTPS for secure communication.

### **4.4 Scalability**
- The system should be designed to scale horizontally by adding more servers as needed.
- The database should be optimized for performance, with indexing and caching where appropriate.

### **4.5 Accessibility**
- The website should meet **WCAG 2.1** accessibility standards, making it usable for people with disabilities.
- Implement keyboard navigation and screen reader compatibility.

---

## **5. System Design**

### **5.1 Database Design**

**Entities:**
1. **User**
   - UserID (PK)
   - Username
   - Email
   - Password (hashed)
   - Role (user/admin)
   
2. **School**
   - SchoolID (PK)
   - SchoolName
   - Address
   - Type (public/private)
   - Website
   - ContactInfo

3. **Review**
   - ReviewID (PK)
   - UserID (FK)
   - SchoolID (FK)
   - Rating
   - Comment
   - DateCreated

4. **Admin Actions**
   - AdminID (PK)
   - ActionType
   - ActionDate

### **5.2 API Endpoints**
1. **POST /register**: Register a new user.
2. **POST /login**: Log in an existing user.
3. **GET /schools**: Search for schools by criteria (name, location).
4. **GET /schools/{id}**: View detailed information about a school.
5. **POST /schools/{id}/review**: Submit a review for a school.
6. **GET /reviews/{school_id}**: Retrieve all reviews for a specific school.
7. **POST /admin/review/approve**: Admin approves a review.
8. **POST /admin/review/reject**: Admin rejects a review.

### **5.3 Frontend Design**

The frontend will include the following pages:
1. **Home Page**: Displays a search bar and trending schools.
2. **School Details Page**: Shows detailed school information along with user reviews and ratings.
3. **Search Results Page**: Allows users to filter and view schools based on different criteria.
4. **Login/Register Page**: Provides authentication functionality.
5. **Admin Dashboard**: Allows admins to manage schools, users, and reviews.

### **5.4 Technologies**
- **Frontend**: React, Axios (for API calls)
- **Backend**: Node.js, Express.js, JWT for authentication
- **Database**: MySQL
- **Authentication**: JWT and bcrypt (password hashing)
- **Deployment**: AWS or Heroku for hosting

---

## **6. Testing**

### **6.1 Types of Testing**
- **Unit Testing**: Individual functions and components will be tested using **Jest** (for React) and **Mocha** (for Node.js).
- **Integration Testing**: Ensuring that frontend and backend components work together.
- **Performance Testing**: Using tools like **Apache JMeter** to test server scalability.
- **Security Testing**: Penetration testing to check for vulnerabilities such as SQL injection and XSS.

---

## **7. Conclusion**

This Software Design Document provides a comprehensive design for the School Rating Website. The system is designed to be scalable, secure, and user-friendly, ensuring that users can easily search for and review schools, while admins can manage the platform effectively.

---
