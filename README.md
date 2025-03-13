# Game Management Web Application

## Project Overview

This is a comprehensive Java web application for a game management system, developed as part of a database design and web development project. The application provides a robust backend for managing game characters, items, weapons, and player interactions using Java Servlets, JSP, and MySQL.

## Technology Stack

- **Programming Language**: Java
- **Web Technologies**: Java Servlets, JSP
- **Database**: MySQL
- **Development Environment**: Eclipse IDE
- **Server**: Apache Tomcat

## Prerequisites

Before you begin, ensure you have the following installed:

1. Java Development Kit (JDK) 8 or higher
2. Eclipse IDE for Enterprise Java and Web Developers
3. Apache Tomcat 9.x
4. MySQL Server
5. MySQL Connector/J

## Project Setup in Eclipse

### 1. Install Required Eclipse Plugins

1. Open Eclipse
2. Go to Help > Eclipse Marketplace
3. Install:
   - Web Tools Platform (WTP)
   - Java EE Developer Tools
   - Maven Integration (if using Maven)

### 2. Database Setup

1. Create a MySQL database:
```sql
CREATE SCHEMA CS5200Project;
USE CS5200Project;
```

2. Run the provided SQL script (`Milestone2_Group2.sql`) to create tables and initial data

### 3. Configure Database Connection

Create a `DatabaseConnection.java` in your project:

```java
package game.dal;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class DatabaseConnection {
    private static final String URL = "jdbc:mysql://localhost:3306/CS5200Project";
    private static final String USER = "your_mysql_username";
    private static final String PASSWORD = "your_mysql_password";
    
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }
}
```

### 4. Add MySQL Connector to Project

1. Download MySQL Connector/J from the official MySQL website
2. In Eclipse:
   - Right-click project > Properties
   - Java Build Path > Libraries
   - Add External JARs
   - Select the MySQL Connector JAR

### 5. Tomcat Server Configuration

#### Option 1: Tomcat Bundled with Project
If Tomcat is already included in your project directory (typically in a folder like `tomcat/` or `apache-tomcat/`):

1. In Eclipse, go to Window > Preferences > Server > Runtime Environments
2. Click "Add"
3. Select "Apache" > "Apache Tomcat v9.0"
4. Browse and select the Tomcat directory in your project
5. Verify the Tomcat installation directory

#### Option 2: Using System-Installed Tomcat
If Tomcat is not in the project:

1. Download Apache Tomcat from the official website
2. Install it on your system
3. In Eclipse, go to Window > Preferences > Server > Runtime Environments
4. Click "Add"
5. Select "Apache" > "Apache Tomcat v9.0"
6. Browse and select your Tomcat installation directory

### Project Tomcat Configuration

1. Right-click project > Properties > Project Facets
2. Enable "Dynamic Web Module"
3. Select the appropriate Tomcat runtime
4. Ensure "Further configuration available" is clicked
5. In the Web Module dialog, set the Content directory (usually `src/main/webapp`)

### Deployment Considerations

- If Tomcat is bundled with the project, include instructions in README about Tomcat location
- Provide guidance on any path-specific configurations
- Mention any environment-specific setup steps

## Project Structure

```
root/
├── database/
│   └── player_database.sql
└── Milestone4/
    └── src/
        └── main/
            ├── java/
            │   └── game/
            │       ├── dal/       # Data Access Layer
            │       ├── model/     # Data Models
            │       └── servlet/   # Web Servlets
            └── webapp/
                ├── WEB-INF/
                │   ├── lib/
                │   │   ├── mysql-connector-java-8.x.x.jar
                │   │   ├── taglibs-standard-impl-1.2.x.jar
                │   │   └── taglibs-standard-spec-1.2.x.jar
                │   └── web.xml
                ├── META-INF/
                ├── images/
                └── *.jsp files
```

### Directory Structure Breakdown

#### Root Directory
- `database/`: Contains SQL scripts for database setup

#### Milestone4 Project Structure
- `src/main/java/`: Java source code
  - `dal/`: Data Access Layer (Data Access Objects)
  - `model/`: Data model classes
  - `servlet/`: Web servlet classes

- `webapp/`: Web application resources
  - `WEB-INF/`: Configuration and library directory
    - `lib/`: External JAR libraries
      - MySQL Connector
      - Taglib libraries
    - `web.xml`: Web application configuration
  - `META-INF/`: Application metadata
  - `images/`: Image resources for the web application
  - `*.jsp`: JavaServer Pages (view layer)

### Library Details in WEB-INF

#### Libraries in WEB-INF/lib/
- `mysql-connector-java-8.x.x.jar`: JDBC driver for MySQL connectivity
- `taglibs-standard-impl-1.2.x.jar`: JSP tag library implementation
- `taglibs-standard-spec-1.2.x.jar`: JSP tag library specifications

#### Additional Web Resources
- `META-INF/`: Contains application metadata
- `images/`: Stores static images used in the web application
- `*.jsp`: Contains the JavaServer Pages for rendering views

### Importing Libraries in Eclipse
1. Right-click project
2. Properties > Java Build Path
3. Libraries tab
4. Add JARs or External JARs
5. Select the libraries from WEB-INF/lib/

### Deployment Considerations
- These libraries will be automatically packaged with the WAR file
- Ensures consistent library versions across different environments

## Key Components

### Data Access Objects (DAOs)
- Implement database operations
- Singleton pattern for connection management
- Key DAOs:
  - `PlayerDao`
  - `CharacterDao`
  - `WeaponDao`
  - `ItemDao`

### Model Classes
- Represent database entities
- Examples:
  - `Player`
  - `Character`
  - `Weapon`
  - `Item`

### Servlets
- Handle HTTP requests
- Interact with DAOs
- Example: `CharacterPage` servlet

## Running the Project

### Project Setup in Eclipse

1. Clone the repository
2. Open Eclipse
3. File > Import > Existing Projects into Workspace
4. Select the project root directory
5. Ensure "Copy projects into workspace" is unchecked

### Tomcat Server Configuration

1. In Eclipse, go to the Servers view
2. Right-click > New > Server
3. Choose Apache > Tomcat version
4. Browse to the Tomcat directory in `servers/`
5. Complete the server configuration wizard

### Starting the Application

1. Ensure all dependencies are resolved
2. Right-click project
3. Run As > Run on Server
4. Select the configured Tomcat server
5. Click "Finish"

### Accessing the Web Application
- Open web browser
- Navigate to `http://localhost:8080/YourProjectName/`

### Potential Setup Issues

#### Common Problems
- Incorrect server path
- Missing Java Build Path configurations
- Incompatible Tomcat version

#### Troubleshooting
1. Verify Java Build Path
   - Right-click project > Properties > Java Build Path
   - Ensure all required libraries are added

2. Check Server Configuration
   - Verify Tomcat directory is correctly specified
   - Restart Eclipse if configuration doesn't take effect

3. Dependency Verification
   - Confirm all required JARs are in the project's `lib/` directory
   - Check MySQL Connector is properly added

## Testing

### Using Driver Class
- `Driver.java` provides comprehensive testing
- Demonstrates CRUD operations
- Helps verify DAO implementations

### Recommended Testing Approach
1. Run Driver class to populate database
2. Test individual servlet functionalities
3. Verify database interactions

## Common Configuration Issues

### JDBC Connection Problems
- Check MySQL server is running
- Verify database credentials
- Ensure MySQL Connector JAR is in build path

### Tomcat Deployment Issues
- Clean and rebuild project
- Verify server runtime configuration
- Check project facets and nature

## Best Practices

1. Always use prepared statements
2. Implement proper exception handling
3. Use connection pooling for performance
4. Secure database credentials

## Logging
- Implement logging (e.g., Log4j)
- Log database operations and errors

## Security Considerations
- Use prepared statements to prevent SQL injection
- Implement input validation
- Secure database connection credentials

## Potential Improvements
- Implement user authentication
- Add more comprehensive error handling
- Create a more interactive frontend
- Implement caching mechanisms

## Contributing

### Code Style
- Follow Java naming conventions
- Use meaningful variable and method names
- Add comments for complex logic

### Pull Request Process
1. Fork the repository
2. Create a feature branch
3. Commit changes
4. Push to your fork
5. Create pull request

## License

## License

### Apache License, Version 2.0

Copyright [Year] [Your Name or Organization]

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

### License Summary

The Apache License 2.0 allows you to:
- Use the software for any purpose
- Distribute modified and unmodified versions
- Modify the software and distribute your modifications
- Use the software commercially

### Contribution Guidelines

By contributing to this project, you agree to license your contributions under the Apache License 2.0.

### Third-Party Libraries

Verify the licenses of all third-party libraries used in the project to ensure compatibility with the Apache License.

## Acknowledgments

Developed as part of a database design course at Northeastern University.

## Contact

For questions or support, contact project contributors.
```

## Troubleshooting Guide

### 1. JDBC Connection Errors
- Verify MySQL is running
- Check connection URL, username, password
- Ensure MySQL Connector JAR is in build path

### 2. Tomcat Deployment Issues
- Clean project (Project > Clean)
- Restart Tomcat
- Verify server runtime configuration

### 3. Database Schema Problems
- Rerun SQL script
- Check for any schema version mismatches
- Verify foreign key constraints

## Additional Resources

- [Eclipse Documentation](https://help.eclipse.org/)
- [Tomcat Documentation](https://tomcat.apache.org/documentation.html)
- [MySQL Connector/J Documentation](https://dev.mysql.com/doc/connector-j/en/)
