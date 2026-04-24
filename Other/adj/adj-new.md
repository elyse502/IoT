### 1. JDBC Delete Operation (Discussion 1)
This code demonstrates how to remove a record from a database. [cite_start]Note that `executeUpdate` is the method used for "Delete" queries[cite: 5, 52].



```java
import java.sql.*;

public class DeleteRecord {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:mysql://localhost/mydatabase?user=root&password="; [cite_start]// [cite: 14, 15]
        
        try {
            [cite_start]// Load Driver and Establish Connection [cite: 14, 16]
            Class.forName("com.mysql.jdbc.Driver");
            Connection con = DriverManager.getConnection(connectionUrl);
            
            [cite_start]// Define SQL command [cite: 51]
            String strSQL = "DELETE FROM students WHERE lastname = 'John'";
            
            [cite_start]// Create statement and execute [cite: 20, 52]
            Statement stmt = con.createStatement();
            int rowsEffected = stmt.executeUpdate(strSQL);
            
            System.out.println(rowsEffected + " rows affected"); [cite_start]// [cite: 53]
            con.close();
        } catch (Exception e) {
            System.out.println("Error: " + e.toString()); [cite_start]// [cite: 40]
        }
    }
}
```

---

### 2. JDBC Update Operation (Discussion 2)
This code shows how to modify existing data. [cite_start]Like the delete operation, it uses `executeUpdate` and returns the count of changed rows[cite: 97].

```java
import java.sql.*;

public class UpdateRecord {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost/mydatabase?user=root&password="; [cite_start]// [cite: 79, 81]
        
        [cite_start]try (Connection con = DriverManager.getConnection(url)) { // [cite: 91]
            Statement stmt = con.createStatement(); [cite_start]// [cite: 93]
            
            [cite_start]// SQL update command to change a student's last name [cite: 95]
            String strSQL = "UPDATE studentS SET lastname = 'John' WHERE firstname = 'KABIBI'";
            
            int rowsEffected = stmt.executeUpdate(strSQL); [cite_start]// [cite: 97]
            System.out.println(rowsEffected + " rows affected"); [cite_start]// [cite: 99]
            
        } catch (SQLException e) {
            System.out.println("SQL Error: " + e.getMessage()); [cite_start]// [cite: 103]
        }
    }
}
```

---

### 3. Java Servlet (Discussion 3)
[cite_start]Based on your screenshot of "Hello World", this is how the Java class behind that page looks [cite: 115-119].



```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.annotation.WebServlet;

[cite_start]// Mapping the servlet to the URL pattern '/hello' [cite: 120]
@WebServlet("/hello")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        
        [cite_start]// This generates the content seen in the browser [cite: 118, 119]
        out.println("<h1>Hello World</h1>");
        out.println("<p>This is my first Servlet</p>");
    }
}
```

---

### 4. JavaServer Page - JSP (Discussion 4)
[cite_start]This shows how to create the dynamic "Hello JSP" page from your materials[cite: 127, 128].

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
    <title>Insert title here</title> </head>
<body>
    <h1>Hello JSP</h1> <p>Now is <%= new java.util.Date() %></p>
</body>
</html>
```

---

### 5. Java Networking (Discussion 5)
[cite_start]This is a standard "Echo" example for Client/Server communication[cite: 129].



**The Server:**
```java
import java.io.*;
import java.net.*;

public class MyServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(8080);
        System.out.println("Server is waiting for client...");
        Socket socket = serverSocket.accept(); // Stops here until a client connects
        
        DataInputStream input = new DataInputStream(socket.getInputStream());
        String message = input.readUTF();
        System.out.println("Client says: " + message);
        
        serverSocket.close();
    }
}
```

**The Client:**
```java
import java.io.*;
import java.net.*;

public class MyClient {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 8080);
        
        DataOutputStream output = new DataOutputStream(socket.getOutputStream());
        output.writeUTF("Hello Server!");
        
        socket.close();
    }
}
```

---

### 6. Hibernate Entity Mapping (Discussion 6)
[cite_start]Hibernate uses annotations to map a class to a table, replacing manual JDBC code[cite: 130].



```java
import javax.persistence.*;

@Entity // Tells Hibernate this class is a table
@Table(name = "students")
public class Student {
    
    @Id // Primary Key
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;
    
    @Column(name = "firstname")
    private String firstName;
    
    @Column(name = "lastname")
    private String lastName;

    // Getters and Setters...
}

/* How it's used in a session:
Session session = sessionFactory.openSession();
Transaction tx = session.beginTransaction();
Student s = new Student();
s.setFirstName("John");
session.save(s); // Hibernate generates the 'INSERT' SQL automatically
tx.commit();
*/
```
