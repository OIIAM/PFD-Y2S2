## Week 14

This week was the week that I decided to start coding out the User creation and authentication portion of the project.

Codes Done:
![alt text](<../Images/Auth.js pt 1.JPG>) ![alt text](<../Images/Auth.js pt 2.JPG>) ![alt text](<../Images/Auth.js pt 3.JPG>) ![alt text](<../Images/AuthController pt 2.JPG>) ![alt text](<../Images/AuthController pt 3.JPG>) ![alt text](<../Images/AuthController pt 5.JPG>) ![alt text](<../Images/AuthController pt 6.JPG>) ![alt text](<../Images/AuthController pt1.JPG>) ![alt text](<../Images/AuthDAL pt 1.JPG>) ![alt text](<../Images/AuthDAL pt 2.JPG>) ![alt text](<../Images/AuthDAL pt 3.JPG>)

AuthController.cs Code explanation:
AuthController.cs contains actions related to authentication, such as signing in users, registering new users, and logging out. Here's an overview of each code block:

Edit and Delete Actions:

Edit: This action handles the HTTP POST request to edit a user. It uses the ValidateAntiForgeryToken to prevent cross-site request forgery (CSRF) attacks. If the operation is successful, it redirects to the Index action; otherwise, it returns the current view.
Delete: Similar to Edit, this action is for deleting a user. It presents the delete view on a GET request and processes the deletion on a POST request, redirecting to the Index upon success.

Sign In Action:

SignIn: This action is invoked on an HTTP POST request when a user attempts to sign in. It doesn't provide the logic for authentication but returns a view named "Auth", for users to enter their credentials.
Log In User Action:

LogInUser: This asynchronous action handles user login. It retrieves a user from the database by email, checks if the retrieved user's password matches the one provided, and if successful, serializes the user data (excluding the password) and sets it in the session before redirecting to the Index or Home action.
Staff Login Action:

StaffLogin: Similar to LogInUser, this action handles staff login. It authenticates the staff member, sets session data, and redirects to a staff-specific dashboard upon successful login.
New User Action:

AddNewUser: This asynchronous action processes the registration of new users. It checks if the model state is valid, hashes the password, saves the user to the database, and redirects to the home page if successful.
AuthController Structure:

The AuthController class provides a structure for the authentication-related actions. It includes methods to display home, index, new user registration, staff login, and user details. It also contains actions to create and edit user details.
Logout Actions:

StaffLogout and LogOut: These actions clear the user's session and redirect to the login or home page, effectively logging the user out of the application.

AuthDAL.cs code explanations:
AuthDAL Initialization:

This class is responsible for initializing the connection to a Firebase Firestore database using a service account JSON file. It sets up the database connection (FirestoreDb db) upon instantiation of AuthDAL.

Get User/Staff By Email:

GetUserByEmail and GetStaffByEmail are asynchronous methods that retrieve a user or staff member from the Firestore database based on the provided email. If a document with the email exists, it is converted to the User or Staff object and returned; otherwise, null is returned, indicating no user/staff was found with that email.

Add User/Staff:

AddUser and AddStaff are asynchronous methods that take a User or Staff object, hash the password for security using BCrypt, and then save this data to the Firestore database within the "users" or "staff" collection. The methods return a boolean indicating the success or failure of the operation.

Get User/Staff:

GetUser and GetStaff are methods that iterate through the Firestore database collection "users" or "staff" and attempt to convert each document into a User or Staff object, which is then added to a list. The process continues until a document with the current ID doesn't exist, at which point the loop exits, and the list of users or staff is returned.

Based on these codes, I was able to get the user creation working. It was mentioned during this week's meeting that the creation of staff should not be displayed anywhere on the website at the moment, however, I decided to have the method for creating the staff within the code first just in case it is needed down the line. The user was able to appear within the Firebase database when creating them. However, when I tried to use the same email to create another account, I was able to create it again, which means that the email authentication part was not working as intended. I kept troubleshooting in an attempt to find the problem, however, as there were no actual errors within the code that would stop it from working properly,![alt text](../Images/image.png) For reference, I was unable to figure out what was wrong with my code.

Thus, after several days of attempted troubleshooting with no results, I decided to ask Vishwa to help me with the code.

While asking Vishwa to help, I was also trying to find out what went wrong with my code.
