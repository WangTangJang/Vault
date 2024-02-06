在Java中连接数据库通常使用JDBC（Java Database Connectivity）技术。以下是连接数据库的基本步骤：
1. **加载数据库驱动程序：**
   ```java
   Class.forName("com.mysql.cj.jdbc.Driver");
   ```
2. **建立数据库连接：**
   ```java
   String url = "jdbc:mysql://localhost:3306/your_database";
   String username = "your_username";
   String password = "your_password";

   Connection connection = DriverManager.getConnection(url, username, password);
   ```
3. **创建Statement对象：**
   通过数据库连接创建一个`Statement`对象，用于执行SQL查询和更新。
   ```java
   Statement statement = connection.createStatement();
   ```
   或者使用`PreparedStatement`来执行**预编译**的SQL语句，这有助于提高性能和防止SQL注入攻击。
   ```java
   String sql = "SELECT * FROM your_table WHERE column = ?";
   PreparedStatement preparedStatement = connection.prepareStatement(sql);
   preparedStatement.setString(1, "some_value");
   ```
4. **执行SQL查询：**
   使用`Statement`或`PreparedStatement`对象执行SQL查询。
   ```java
   ResultSet resultSet = statement.executeQuery("SELECT * FROM your_table");
   ```
   对于更新操作（如插入、更新、删除），可以使用`executeUpdate()`方法。
   ```java
   int rowsAffected = statement.executeUpdate("UPDATE your_table SET column = 'new_value' WHERE id = 1");
   ```
5. **处理结果集：**
   如果执行的是查询操作。
   ```java
   while (resultSet.next()) {
       // 处理每一行的数据
       String value = resultSet.getString("column_name");
       // 具体操作...
   }
   ```
6. **关闭资源：**
   ```java
   resultSet.close();
   statement.close();
   connection.close();
   ```