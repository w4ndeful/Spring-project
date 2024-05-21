Functional Requirements

1. **User Authentication**:
   - Users must be able to register and log in.
   - Admin users must be able to manage other user accounts.

2. **Warranty Registration**:
   - Users must be able to register new warranty cards.
   - Each warranty card must include details such as equipment name, serial number, warranty start date, and warranty end date.

3. **Warranty Search**:
   - Users must be able to search for warranty cards by equipment name, serial number, or date range.

4. **Warranty Update**:
   - Users must be able to update the details of existing warranty cards.

5. **Warranty Deletion**:
   - Users must be able to delete warranty cards.

6. **Warranty Expiry Notification**:
   - The system must notify users when a warranty is about to expire (e.g., via email or dashboard alert).

7. **User Roles and Permissions**:
   - Define different roles (e.g., admin, user) with specific permissions.

8. **Report Generation**:
   - Users must be able to generate reports of warranty cards within a specific date range.

9. **Audit Trail**:
   - The system must keep a log of all changes made to warranty cards for auditing purposes.

10. **Dashboard Overview**:
    - Users must have access to a dashboard that provides an overview of the total warranties, upcoming expiries, and recent activities.

### Mockups

#### 1. Login Page
![Login Page](mockup-login.png)

#### 2. Dashboard
![Dashboard](mockup-dashboard.png)

#### 3. Warranty Registration Form
![Warranty Registration Form](mockup-warranty-registration.png)

#### 4. Warranty Search Results
![Warranty Search Results](mockup-warranty-search.png)

#### 5. Warranty Details View
![Warranty Details View](mockup-warranty-details.png)

#### 6. Update Warranty Form
![Update Warranty Form](mockup-update-warranty.png)

#### 7. Delete Warranty Confirmation
![Delete Warranty Confirmation](mockup-delete-warranty.png)

#### 8. Report Generation Form
![Report Generation Form](mockup-report-generation.png)

#### 9. User Management (Admin)
![User Management](mockup-user-management.png)

#### 10. Audit Trail View
![Audit Trail View](mockup-audit-trail.png)

### System Behavior and REST API Endpoints

#### Authentication

1. **Register User**
   - **Endpoint**: `POST /api/auth/register`
   - **Request Body**:
     ```json
     {
       "username": "string",
       "password": "string",
       "role": "string" // e.g., "user" or "admin"
     }
     ```
   - **Response**: 
     ```json
     {
       "message": "User registered successfully",
       "userId": "string"
     }
     ```

2. **Login User**
   - **Endpoint**: `POST /api/auth/login`
   - **Request Body**:
     ```json
     {
       "username": "string",
       "password": "string"
     }
     ```
   - **Response**:
     ```json
     {
       "token": "string"
     }
     ```

#### Warranty Management

3. **Create Warranty**
   - **Endpoint**: `POST /api/warranties`
   - **Request Body**:
     ```json
     {
       "equipmentName": "string",
       "serialNumber": "string",
       "warrantyStartDate": "date",
       "warrantyEndDate": "date"
     }
     ```
   - **Response**:
     ```json
     {
       "message": "Warranty created successfully",
       "warrantyId": "string"
     }
     ```

4. **Get Warranty by ID**
   - **Endpoint**: `GET /api/warranties/{id}`
   - **Response**:
     ```json
     {
       "warrantyId": "string",
       "equipmentName": "string",
       "serialNumber": "string",
       "warrantyStartDate": "date",
       "warrantyEndDate": "date"
     }
     ```

5. **Search Warranties**
   - **Endpoint**: `GET /api/warranties`
   - **Query Parameters**: `equipmentName`, `serialNumber`, `startDate`, `endDate`
   - **Response**:
     ```json
     [
       {
         "warrantyId": "string",
         "equipmentName": "string",
         "serialNumber": "string",
         "warrantyStartDate": "date",
         "warrantyEndDate": "date"
       }
     ]
     ```

6. **Update Warranty**
   - **Endpoint**: `PUT /api/warranties/{id}`
   - **Request Body**:
     ```json
     {
       "equipmentName": "string",
       "serialNumber": "string",
       "warrantyStartDate": "date",
       "warrantyEndDate": "date"
     }
     ```
   - **Response**:
     ```json
     {
       "message": "Warranty updated successfully"
     }
     ```

7. **Delete Warranty**
   - **Endpoint**: `DELETE /api/warranties/{id}`
   - **Response**:
     ```json
     {
       "message": "Warranty deleted successfully"
     }
     ```

#### Notification and Reporting

8. **Get Expiring Warranties**
   - **Endpoint**: `GET /api/warranties/expiring`
   - **Query Parameters**: `days` (number of days before expiry)
   - **Response**:
     ```json
     [
       {
         "warrantyId": "string",
         "equipmentName": "string",
         "serialNumber": "string",
         "warrantyEndDate": "date"
       }
     ]
     ```

9. **Generate Report**
   - **Endpoint**: `GET /api/reports/warranties`
   - **Query Parameters**: `startDate`, `endDate`
   - **Response**:
     ```json
     [
       {
         "warrantyId": "string",
         "equipmentName": "string",
         "serialNumber": "string",
         "warrantyStartDate": "date",
         "warrantyEndDate": "date"
       }
     ]
     ```

#### Audit and User Management

10. **Get Audit Trail**
    - **Endpoint**: `GET /api/audit`
    - **Response**:
      ```json
      [
        {
          "action": "string",
          "username": "string",
          "timestamp": "datetime",
          "details": "string"
        }
      ]
      ```

11. **Manage Users (Admin)**
    - **Endpoint**: `GET /api/users`
    - **Response**:
      ```json
      [
        {
          "userId": "string",
          "username": "string",
          "role": "string"
        }
      ]
      ```

    - **Endpoint**: `PUT /api/users/{id}`
    - **Request Body**:
      ```json
      {
        "username": "string",
        "role": "string"
      }
      ```
    - **Response**:
      ```json
      {
        "message": "User updated successfully"
      }
      ```

    - **Endpoint**: `DELETE /api/users/{id}`
    - **Response**:
      ```json
      {
        "message": "User deleted successfully"
      }
      ```
