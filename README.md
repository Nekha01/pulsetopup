An Intuitive Online Mobile Recharge Portal with Multi-Provider Support, Secure Transactions, and Real-Time Updates



1. Introduction

This document outlines the requirements for the Online Mobile Recharge Portal, which provides users with a seamless platform to recharge mobile accounts across multiple providers. The system ensures secure transactions, real-time updates, and an intuitive interface for users to manage their accounts.



2. Functional Requirements



User Registration and Authentication

Users must be able to register with a username, email, and password.
Secure login functionality using JWT-based authentication.
Mobile Recharge Service

Users can select from multiple mobile service providers.
Recharge requests are processed securely with real-time updates on the status (success, pending, failure).
Transaction History

Users can view past transactions with details such as date, amount, and provider.
Notifications

Users receive confirmation emails or messages after recharge completion.
Real-time alerts for transaction status updates.
Payment Gateway Integration

Securely process payments via integrated external gateways.
Provider Management

Admins can add, update, or remove supported mobile providers.


3. Non-Functional Requirements

Performance

The system must handle 100 concurrent user transactions with a response time of under 3 seconds.
Scalability

The architecture must support easy addition of new mobile providers and an increasing user base.
Security

All sensitive data (e.g., passwords, payment information) must be encrypted using AES standards.
Authentication tokens must be securely managed using HTTPS.
Availability

The system should provide 99.9% uptime.
Usability

The interface should be user-friendly with minimal steps to complete a recharge.
Maintainability

Code must adhere to best practices, ensuring ease of updates and debugging.
Compliance

The system must comply with local and international data protection regulations (e.g., GDPR, PCI-DSS).


4. References

1.      Spring Boot Documentation

2.      JWT Authentication Standards

3.      AES Encryption Standards

4.      Payment Gateway Integration Guides (e.g., Stripe/PayPal)



Sample Websites/Applications for Reference

Paytm
https://www.paytm.com
Offers multi-provider mobile recharges with secure payment options and real-time status updates.
Freecharge
https://www.freecharge.in
A simple platform for mobile recharges with history management and notifications.
Mobikwik
https://www.mobikwik.com
Supports multiple providers and secure payment integrations, along with user-friendly interfaces.
Airtel Thanks App
https://www.airtel.in/thanks-app
Focused on providing seamless mobile recharge services for Airtel users with secure transactions and real-time updates.
MyJio App
https://www.jio.com/myjio-app
Offers mobile recharge services exclusively for Jio users, with transaction history and notification features.
Google Pay (Recharge Feature)
https://pay.google.com
Provides a secure recharge option with multi-provider support and real-time status updates.




Project Summary: Online Mobile Recharge Portal
The Mobile Recharge Application System is a Spring Boot application designed to manage Users and plans effectively. The system includes features for managing Users, History, and RechargePlans. Key functionalities include CRUD operations, pagination, sorting, and JPQL queries for optimized data access. The project adheres to best practices by leveraging modular design and annotations for maintainability.

Modules and Features:
Entities: Define relationships and attributes.
Repositories: Enable data access and querying using Spring Data JPA.
CRUD Operations: Comprehensive functionality to create, read, update, and delete records.
Pagination and Sorting: Implemented for efficient data management and presentation.
JPQL Queries: Provide custom methods for advanced data retrieval.
Swagger Integration: Offers interactive API documentation for testing endpoints.
AOP Integration: Implements logging and method-level aspect-oriented programming (AOP) configurations.
Logging: Logs application events for debugging and monitoring.
Annotations: Includes Lombok for boilerplate code reduction and JSON annotations for serialization/deserialization.
Test Cases: Extensive JUnit tests to validate controllers, repositories, annotations, and configurations.
This project ensures scalability and ease of use, making it suitable for varying-size libraries. It follows industry standards and practices for robust application development.

Entities and Attributes
User
id (Primary Key)
username
password
email
firstName
lastName
phoneNumber
address
histories (One-to-many relationship with History)
rechargePlans (Many-to-many relationship with RechargePlan)
RechargePlan
id (Primary Key)
planName
planDescription
planDuration
price
users (Many-to-many relationship with User)
History
id (Primary Key)
userId (Foreign Key, many-to-one relationship with User)
rechargePlan
date
time
user (Many-to-one relationship with User)

Relationships
User ↔ History
Type: One-to-Many
Explanation: Each User can have multiple History records, but each History record belongs to one User.
Mapping:
User has @OneToMany(mappedBy = "user")
History has @ManyToOne
User ↔ RechargePlan
Type: Many-to-Many
Explanation: Each User can have multiple RechargePlans, and each RechargePlan can be linked to multiple Users.
Mapping:
User has @ManyToMany
RechargePlan has @ManyToMany(mappedBy = "users")
History ↔ User
Type: Many-to-One
Explanation: Each History record belongs to one User, and each User can have multiple History records.
Mapping:
History has @ManyToOne
User has @OneToMany(mappedBy = "user")


ER Diagram

[User] ----< (1-to-Many) >---- [History]

[User] ----< (Many-to-Many) >---- [RechargePlan]


UserController


Base URL: /api/users

POST /api/users
Description: Creates a new user.
Request Body: User object (JSON)
Response: User object (JSON)
Status Codes:
201 Created – When the user is successfully created.
GET /api/users/{id}
Description: Retrieves a user by ID.
Request Params: id (Long) - User ID
Response: User object (JSON) if found.
Status Codes:
200 OK – When the user is found.
404 Not Found – When the user is not found.
GET /api/users/paginate
Description: Retrieves users with pagination and sorting options.
Request Params:
page (int) - Page number (default: 0)
size (int) - Page size (default: 10)
sortBy (String) - Sorting field (default: id)
sortOrder (String) - Sorting order (default: asc)
Response: A paginated list of users.
Status Codes:
200 OK – When the users are retrieved successfully.
GET /api/users
Description: Retrieves all users.
Response: List of User objects (JSON)
Status Codes:
200 OK – When the users are retrieved successfully.
PUT /api/users/{id}
Description: Updates an existing user.
Request Params: id (Long) - User ID
Request Body: User object (JSON)
Response: Updated User object (JSON)
Status Codes:
200 OK – When the user is updated successfully.
404 Not Found – When the user is not found.
DELETE /api/users/{id}
Description: Deletes a user by ID.
Request Params: id (Long) - User ID
Response: No content.
Status Codes:
204 No Content – When the user is deleted successfully.
404 Not Found – When the user is not found.
RechargePlanController
Base URL: /RechargePlan
POST /RechargePlan
Description: Create a new recharge plan.
Request Body: RechargePlan object (JSON)
Response: RechargePlan object (JSON)
Status Codes:
201 Created – When the recharge plan is created successfully.
GET /RechargePlan
Description: Retrieves all recharge plans.
Response: List of RechargePlan objects (JSON)
Status Codes:
200 OK – When the recharge plans are retrieved successfully.
GET /RechargePlan/{id}
Description: Retrieves a recharge plan by ID.
Request Params: id (Long) - Recharge Plan ID
Response: RechargePlan object (JSON)
Status Codes:
200 OK – When the recharge plan is found.
404 Not Found – When the recharge plan is not found.
PUT /RechargePlan/{id}
Description: Updates an existing recharge plan.
Request Params: id (Long) - Recharge Plan ID
Request Body: RechargePlan object (JSON)
Response: Updated RechargePlan object (JSON)
Status Codes:
200 OK – When the recharge plan is updated successfully.
404 Not Found – When the recharge plan is not found.
DELETE /RechargePlan/{id}
Description: Deletes a recharge plan by ID.
Request Params: id (Long) - Recharge Plan ID
Response: No content.
Status Codes:
204 No Content – When the recharge plan is deleted successfully.
404 Not Found – When the recharge plan is not found.

HistoryController
Base URL: /History

POST /History
Description: Creates a new history record.
Request Body: History object (JSON)
Response: History object (JSON)
Status Codes:
201 Created – When the history record is created successfully.
GET /History
Description: Retrieves all history records.
Response: List of History objects (JSON)
Status Codes:
200 OK – When the history records are retrieved successfully.
GET /History/{id}
Description: Retrieves a history record by ID.
Request Params: id (Long) - History record ID
Response: History object (JSON)
Status Codes:
200 OK – When the history record is found.
404 Not Found – When the history record is not found.
PUT /History/{id}
Description: Updates an existing history record.
Request Params: id (Long) - History record ID
Request Body: History object (JSON)
Response: Updated History object (JSON)
Status Codes:
200 OK – When the history record is updated successfully.
404 Not Found – When the history record is not found.
DELETE /History/{id}
Description: Deletes a history record by ID.
Request Params: id (Long) - History record ID
Response: No content.
Status Codes:
204 No Content – When the history record is deleted successfully.
404 Not Found – When the history record is not found.


Dummy JSON data for each entity in the Online Mobile Recharge Portal project:

User:

{

 "id": 1,

 "username": "john_doe",

 "password": "password123",

 "email": "john.doe@example.com",

 "firstName": "John",

 "lastName": "Doe",

 "phoneNumber": "9876543210",

 "address": "1234 Elm Street, Springfield"

}



RechargePlan:

{

 "id": 1,

 "planName": "Plan A",

 "planDescription": "Basic recharge plan",

 "planDuration": 30,

 "price": 10.0,

 "users": [

  {

   "id": 1,

   "username": "john_doe",

   "email": "john.doe@example.com"

  },

  {

   "id": 2,

   "username": "jane_smith",

   "email": "jane.smith@example.com"

  }

 ]

}



History:

{

 "id": 1,

 "userId": 1,

 "rechargePlan": "Plan A",

 "date": "2025-01-01",

 "time": "10:00 AM",

 "user": {

  "id": 1,

  "username": "john_doe",

  "firstName": "John",

  "lastName": "Doe"

 }

}

These JSON data examples provide a clear representation of how the entities User, RechargePlan, and History would be structured in your system. Each entity contains relevant attributes and demonstrates the relationships between them (such as the one-to-many and many-to-many relationships).

