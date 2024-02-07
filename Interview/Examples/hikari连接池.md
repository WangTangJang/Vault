```java
package demo.connectionpool;  
  
import com.zaxxer.hikari.HikariConfig;  
import com.zaxxer.hikari.HikariDataSource;  
  
import javax.sql.DataSource;  
import java.sql.Connection;  
import java.sql.ResultSet;  
import java.sql.SQLException;  
import java.sql.Statement;  
  
public class demo {  
    public static void main(String[] args) {  
        HikariConfig config = new HikariConfig();  
        config.setJdbcUrl("jdbc:mysql://localhost:3306/test");  
        config.setUsername("root");  
        config.setPassword("20020525");  
        config.addDataSourceProperty("connectionTimeout", "1000");// 连接超时：1秒  
        config.addDataSourceProperty("idleTimeout", "1000");// 空闲超时：60秒  
        config.addDataSourceProperty("maximumPoolSize", "10");// 最大连接数：10  
  

        DataSource ds = new HikariDataSource(config);  
  
        String sql = "select * from users";  
        String sql2= "select * from orders";  
        try (Connection connection = ds.getConnection()){  
            Statement statement1 = connection.createStatement();  
            ResultSet resultSet = statement1.executeQuery(sql);  
            while (resultSet.next()){  
                System.out.println(resultSet.getString("username"));  
            }  
            statement1.close();  
            // 程序暂停三秒  
            try {  
                System.out.println("stopping....");  
                for (int i = 3; i>0; i--){  
                    System.out.println(i);  
                    Thread.sleep(1000);  
                }  
            } catch (InterruptedException e) {  
                e.printStackTrace();  
            }  
            Statement statement2 = connection.createStatement();  
            ResultSet resultSet2 = statement2.executeQuery(sql2);  
            while (resultSet2.next()){  
                System.out.println(resultSet2.getString("order_number"));  
            }  
        }catch (SQLException e){  
            e.printStackTrace();  
        }  
    }  
}
```