
# Chess Game Backend

This project involves the backend implementation of a chess game using MySQL, JDBC, Eclipse, and Tomcat Server, with key features including game history tracking, player profiles and leaderboard management, matchmaking and scheduling, tournament organization, persistent game state storage, user notifications and messaging, and analytics and reporting for performance insights.



## Table of Contents





 - [Project Setup](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Requirements](https://github.com/matiassingers/awesome-readme)
 - [How to Run the Project](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)
 - [Database Schema](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)
 - [API Endpoints](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)
 - [Error Handling](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)
 - [Contributing](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)


#  Project Setup
## 1. Clone the Repository
git clone https://github.com/praveen66660/user-app.git
cd user-app

### 2. Set Up the Database

1. **Install MySQL**: Ensure MySQL is installed on your system. You can download it from [MySQL's official website](https://dev.mysql.com/downloads/mysql/).

2. **Create the Database**:

   ```sql
   CREATE DATABASE IF NOT EXISTS chessgame;
   USE chessgame;
   ```

3. **Run the SQL Script**: Execute the SQL script provided in the `sql` directory to create the necessary tables.

   ```sql
   -- Drop existing tables if they exist
   DROP TABLE IF EXISTS game_history;
   DROP TABLE IF EXISTS games;
   DROP TABLE IF EXISTS users;

   -- Create tables
   CREATE TABLE users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       username VARCHAR(50) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       email VARCHAR(100) NOT NULL
   );

   CREATE TABLE games (
       id INT AUTO_INCREMENT PRIMARY KEY,
       player1_id INT NOT NULL,
       player2_id INT NOT NULL,
       game_state TEXT NOT NULL,
       FOREIGN KEY (player1_id) REFERENCES users(id) ON DELETE CASCADE,
       FOREIGN KEY (player2_id) REFERENCES users(id) ON DELETE CASCADE
   );

   CREATE TABLE game_history (
       id INT AUTO_INCREMENT PRIMARY KEY,
       game_id INT NOT NULL,
       move_number INT NOT NULL,
       move_description VARCHAR(255) NOT NULL,
       FOREIGN KEY (game_id) REFERENCES games(id) ON DELETE CASCADE
   );
   ```
## 3. Set Up Eclipse
#### 1. Install Eclipse: Download and install Eclipse IDE for Java Developers from Eclipse's official website.

#### 2. Import the Project
- Open Eclipse.
- Go to File > Import.
- Select General > Existing Projects into Workspace.
- Browse to the cloned repository and select the project.
- Click Finish.

## 4. Set Up Tomcat Server
#### 1. Install Tomcat: Download and install Apache Tomcat from Tomcat's official website.

#### 2. Configure Tomcat in Eclipse:
- Go to Window > Preferences > Server > Runtime Environments.
- Click Add and select Apache Tomcat.
- Browse to the Tomcat installation directory and click Finish.

#### 3. Add Tomcat Server:

- Go to Window > Show View > Servers.
- Right-click in the Servers view and select New > Server.
- Select the Tomcat server you configured and click Finish.

### 5. Configure Database Connection

Update the `DatabaseConnection.java` file with your MySQL database credentials:

```java
package com.chessgame.util;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/chess_game";
    private static final String USER = "root";
    private static final String PASSWORD = "osama";

    public static Connection getConnection() throws SQLException {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            return DriverManager.getConnection(URL, USER, PASSWORD);
        } catch (ClassNotFoundException e) {
            throw new SQLException("MySQL Driver not found", e);
        }
    }
}
```

# Requirements
- Java Development Kit (JDK) 8 or higher
- MySQL Server 5.7 or higher
- Eclipse IDE for Java Developers
- Apache Tomcat 9.0 or higher
- MySQL Connector/J (included in the project)


# How to Run the Project
#### 1. Start MySQL Server: Ensure your MySQL server is running.

#### 2. Deploy the Project:

- Right-click on the project in Eclipse.
- Select Run As > Run on Server.
- Choose the Tomcat server you configured and click Finish.

#### 3. Access the Application:

- Open your web browser and go to http://localhost:8080/chessgame-backend

# Database schema
- The database schema includes the following    tables:

- users: Stores user information.
- games: Stores game information.
- game_history: Stores game history (moves).


## API Endpoints
### user


- POST /users/create: Create a new user :-
  Request Body: { "username": "player1",     "password": "pass123", "email": "player1@example.com" }
- GET /users/{username}: Get user by username.
- PUT /users/{id}: Update user information.
- DELETE /users/{id}: Delete user by ID.


## Games
- POST /games/create: Create a new game.
Request Body: { "player1Id": 1, "player2Id": 2, "gameState": "Initial state" }
- GET /games/{id}: Get game by ID.
- PUT /games/{id}: Update game state.
- DELETE /games/{id}: Delete game by ID.
## Game History
- POST /game-history/add: Add a move to the    game history.
- Request Body: { "gameId": 1, "moveNumber": 1, "moveDescription": "e2 to e4" }
- GET /game-history/{gameId}: Get game    history by game ID.
- DELETE /game-history/{gameId}: Delete game history by game ID.

## Error Handling
The project includes error handling for database-related errors and general exceptions. Specific errors such as duplicate username or email are caught and handled gracefully.

# Chess Game Login Page

This project includes the HTML code for a login page of an online chess game. It allows users to log into the game platform by providing their email and password. The page is designed with a clean and modern layout, including responsive design features and basic navigation.

## Features
- **Login Form**: A form where users can enter their email and password.
- **Navigation**: Links to the Home, About, and Help pages for easy site navigation.
- **Responsive Design**: The page is designed to be responsive, making it user-friendly across devices.
- **Styling**: Basic CSS for a sleek design with background image support and modern form elements.
- **Footer**: Contains useful links and a call to action for users who don't have an account yet.


## HTML Structure
- `<header>`: Contains the site's navigation links (Home, About, Help).
- `<nav>`: Holds a list of navigation links, which are styled to be displayed as inline items.
- `<main>`: The main content area containing the login form, where users can input their credentials.
- `<footer>`: Contains additional links like "Don't have an account? Register".

## Code Overview

### HTML Markup
The page structure includes semantic HTML elements such as `<header>`, `<nav>`, `<main>`, and `<footer>` to ensure accessibility and SEO benefits.  
A login form (`<form>`) with email and password input fields is created within the `<main>` content area.  
Navigation links are placed in a simple horizontal layout in the `<header>`.

### CSS Styling
- **General Layout**: The page uses a fixed background image and centered text to create an attractive, modern look.
- **Form Styles**: The login form is styled with padding, border-radius, and background color, making it visually distinct and user-friendly.
- **Responsive Design**: The page adapts to different screen sizes, ensuring a consistent user experience across devices.

## Example Code:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login - Chess Game</title>
    <style>
        /* General Styles */
        body {
            font-family: 'Arial', sans-serif;
            color: rgb(2, 0, 0);
            background-image: url(bg.jpg);
            background-size: cover;
            background-position: center top;
            background-attachment: fixed;
            margin: 0;
            padding: 0;
        }

        header, footer {
            background-color: #111518;
            padding: 10px;
            text-align: center;
        }

        nav ul {
            list-style: none;
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 10px 0;
        }

        nav ul li a {
            text-decoration: none;
            color: rgb(245, 242, 242);
            font-size: 1.1rem;
        }

        nav ul li a:hover {
            text-decoration: underline;
        }

        .main-content {
            padding: 20px;
            text-align: center;
        }

        footer p {
            margin: 5px 0;
        }

        footer form input[type="email"] {
            padding: 10px;
            border: none;
            border-radius: 5px;
        }

        footer form button {
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
        }

        .login-form {
            max-width: 400px;
            margin: 50px auto;
            background: transparent;
            padding: 20px;
            border-radius: 8px;
            color: rgb(244, 241, 241);
        }

        .login-form input[type="email"],
        .login-form input[type="password"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #150505;
            border-radius: 10px;
        }

        .login-form button {
            width: 100%;
            padding: 10px;
            background-color: rgb(48, 202, 5);
            color: rgb(252, 251, 252);
            border: none;
            border-radius: 20px;
        }
    </style>
</head>

<body>

    <header>
        <nav>
            <ul>
                <li><a href="index.html">Home</a></li>
                <li><a href="about.html">About</a></li>
                <li><a href="help.html">Help</a></li>
            </ul>
        </nav>
    </header>

    <div class="main-content">
        <h1>Login</h1>
        <form class="login-form">
            <input type="email" placeholder="Email ID" required>
            <input type="password" placeholder="Password" required>
            <button type="submit">Login</button>
        </form>
    </div>
    <div>
        <p>Don't have an account? <a href="#">Register</a></p>
    </div>

</body>

</html>
```

# CSS Styling for Form and Page Layout

This CSS file provides styling for a basic webpage with a form. It includes a background image, form layout, input field styling, and button customization. The form elements are responsive and visually appealing, with hover effects and error message styling.

## Features

- **Global Styles**: Applies background image and font settings across the page.
- **Form Styling**: Styles a form with a background image, padding, border-radius, and box-shadow for a modern look.
- **Input Fields**: Customizes input, select, and textarea elements for consistent styling across the form.
- **Button Customization**: Includes submit, reset, and checkbox button styles with hover effects for interactivity.
- **Error Message Styling**: Red-colored error messages for form validation feedback to ensure user-friendly form validation.

## Key Styles

- **Text Inputs**: Full-width inputs with padding, rounded borders, and consistent styling.
- **Buttons**: A green submit button, a red reset button, and styled checkboxes with hover effects.
- **Form Layout**: A centered form with a clean, modern design enhanced by shadow effects to stand out.

## How to Use

1. **Link the CSS to Your HTML**  
   Link the provided `style.css` file to your HTML file within the `<head>` section like this:
   ```html
   <link rel="stylesheet" href="style.css">``` 


# JavaScript Validation for Form

This JavaScript file contains functions to validate form inputs for both registration and login forms. It ensures that users enter valid data before the form can be submitted.

## Features

- **Form Validation**: Validates fields such as name, address, email, password, subject, and agreement checkbox for the registration form.
- **Login Validation**: Validates email and password fields in the login form to ensure they meet required conditions.
- **Error Messages**: Displays relevant error messages next to invalid form fields to guide the user.
- **Custom Validation Logic**:
  - Name: Must not be empty and should not contain numbers.
  - Address: Must not be empty.
  - Email: Must be a valid email with `@`.
  - Password: Must be at least 8 characters long.
  - Subject: Must not be empty (for registration).
  - Agree: Checkbox must be checked (for registration).

## Functions

### `validateForm()`
Validates the registration form:
- Ensures the fields for name, address, email, password, subject, and agreement are properly filled in.
- Returns `true` if all fields are valid, otherwise `false` and displays error messages.

```javascript
function validateForm() {
    const name = document.getElementById("name").value;
    const address = document.getElementById("address").value;
    const email = document.getElementById("email").value;
    const password = document.getElementById("password").value;
    const subject = document.getElementById("subject").value;
    const agree = document.getElementById("agree").checked;
    const nameError = document.getElementById("name-error");
    const addressError = document.getElementById("address-error");
    const emailError = document.getElementById("email-error");
    const passwordError = document.getElementById("password-error");
    const subjectError = document.getElementById("subject-error");
    const agreeError = document.getElementById("agree-error");

    nameError.textContent = "";
    addressError.textContent = "";
    emailError.textContent = "";
    passwordError.textContent = "";
    subjectError.textContent = "";
    agreeError.textContent = "";

    let isValid = true;

    if (name === "" || /\d/.test(name)) {
        nameError.textContent = "Please enter your name properly";
        isValid = false;
    }
    if (address === "") {
        addressError.textContent = "Please enter your address";
        isValid = false;
    }
    if (email === "" || !email.includes("@")) {
        emailError.textContent = "Please enter a valid email id";
        isValid = false;
    }
    if (password === "" || password.length < 8) {
        passwordError.textContent = "Please enter a password with atleast 8 characters";
        isValid = false;
    }
    if (subject === "") {
        subjectError.textContent = "Please enter your course.";
        isValid = false;
    }
    if (!agree) {
        agreeError.textContent = "Please agree to the above information";
        isValid = false;
    }

    return isValid;
}
```

# loginCheck Function

## Description

The `loginCheck()` function is used to validate the login form by checking two key fields: the email and the password.

### Functionality

- **Email Validation**: Ensures the email entered is in a valid format.
- **Password Validation**: Ensures the password is at least 8 characters long.
- **Return Values**:
  - Returns `true` if both the email and password meet the validation criteria.
  - Returns `false` and displays appropriate error messages if either field is invalid.

## Usage

```javascript
function loginCheck() {
    // Email and password validation logic here
}
```

## loginCheck()
#### Validates the login form:

- *Ensures the `email` field is not empty and contains a valid `email` format.*

- *Validates the `password` to ensure it is at least 8 characters long.*

Returns `true` if both fields are valid, otherwise `false` and displays error messages next to the respective fields.






