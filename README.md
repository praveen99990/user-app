
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

## 5. Configure Database Connection
Update the DatabaseConnection.java file with your MySQL database credentials

```http
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

