# Java Database Connectivity

[TOC]

# 快速入门

**JDBC** 全称是 **Java 数据库连接**（Java Database Connectivity）。它是一个标准的 Java API（由一组接口和类组成），允许 Java 程序使用 SQL（结构化查询语言）连接并与各种关系型数据库（如 MySQL, PostgreSQL, Oracle, SQL Server 等）进行交互。

最关键的一点是：**JDBC 是一个规范（一套接口），而不是一个实现**。它定义了“该如何做”，但本身不完成具体工作。具体的工作由各个数据库厂商提供的 **JDBC 驱动** 来完成。

```java
public class JDBCDemo {
    public static void main(String[] args) throws Exception {
        // 注册驱动
        Class.forName("com.mysql.jdbc.Driver");
        
        // 获取连接
        String url = "jdbc:mysql://127.0.0.1:3306/mydb";
        String username = "root";
        String password = "1234";
        Connection conn = DriverManager.getConnection(url, username, password);
        
        // 执行sql
        String sql = "SELECT id, name FROM users";
        Statement stmt = conn.createStatement();
        ResultSet rs = stmt.executeQuery(sql);
        // 然后遍历结果集处理数据
		while (rs.next()) {
		    int id = rs.getInt("id");
		    String name = rs.getString("name");
		    System.out.println("ID: " + id + ", Name: " + name);
		}
        
        // 关闭资源
        stmt.close();
        conn.close();
    }
}
```



# DriverManager

`DriverManager` 是 JDBC API 中的一个**核心类**，位于 `java.sql` 包中。它充当一个**管理层**，主要负责：

1.  **加载和注册** JDBC 驱动程序
2.  **建立**与数据库的连接
3.  **管理**已注册的驱动程序

## 主要功能和方法

### 1. 注册驱动 (Registering Drivers)

虽然现代 JDBC 驱动大多可以自动注册，但了解手动注册方式很重要。

**传统方式（JDBC 4.0 之前）：**
```java
// 通过 Class.forName() 加载驱动类，驱动静态代码块会自动向 DriverManager 注册自己
Class.forName("com.mysql.cj.jdbc.Driver");
```

**自动注册（JDBC 4.0+）：**
只要将驱动的 JAR 文件放在类路径下，DriverManager 会自动发现并加载 `META-INF/services/java.sql.Driver` 文件中指定的驱动类。

### 2. 获取连接 (Getting Connections)

这是 DriverManager 最常用的功能。

**基本用法：**
```java
String url = "jdbc:mysql://localhost:3306/mydb";
String user = "root";
String password = "password";

// 获取连接的基本方法
Connection conn = DriverManager.getConnection(url, user, password);

// 也可以将用户名和密码包含在 URL 中
String urlWithAuth = "jdbc:mysql://localhost:3306/mydb?user=root&password=password";
Connection conn2 = DriverManager.getConnection(urlWithAuth);

// 使用 Properties 对象传递参数
Properties props = new Properties();
props.setProperty("user", "root");
props.setProperty("password", "password");
props.setProperty("useSSL", "false");
Connection conn3 = DriverManager.getConnection(url, props);
```

### 3. 管理驱动

```java
// 获取所有已注册的驱动枚举
Enumeration<Driver> drivers = DriverManager.getDrivers();
while (drivers.hasMoreElements()) {
    Driver driver = drivers.nextElement();
    System.out.println("驱动类: " + driver.getClass().getName());
}

// 手动注册驱动（通常不需要）
Driver mysqlDriver = new com.mysql.cj.jdbc.Driver();
DriverManager.registerDriver(mysqlDriver);

// 注销驱动
DriverManager.deregisterDriver(mysqlDriver);
```

## 完整工作流程示例

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.Properties;

public class DriverManagerDemo {
    public static void main(String[] args) {
        // 数据库配置
        String url = "jdbc:mysql://localhost:3306/mydb";
        String user = "root";
        String password = "1234";
        
        Connection conn = null;
        Statement stmt = null;
        ResultSet rs = null;
        
        try {
            // 1. 自动注册驱动（JDBC 4.0+ 特性）
            // 不需要显式调用 Class.forName()，只要mysql驱动jar在类路径中即可
            
            // 2. 获取数据库连接 - DriverManager 的核心功能
            System.out.println("正在尝试连接数据库...");
            conn = DriverManager.getConnection(url, user, password);
            
            // 3. 验证连接是否成功
            if (conn != null && !conn.isClosed()) {
                System.out.println("数据库连接成功！");
                
                // 4. 执行简单查询
                stmt = conn.createStatement();
                rs = stmt.executeQuery("SELECT 1 as test");
                
                if (rs.next()) {
                    System.out.println("测试查询成功，结果: " + rs.getInt("test"));
                }
            }
            
        } catch (Exception e) {
            System.err.println("数据库连接失败: " + e.getMessage());
            e.printStackTrace();
        } finally {
            // 关闭资源
            try {
                if (rs != null) rs.close();
                if (stmt != null) stmt.close();
                if (conn != null) conn.close();
                System.out.println("数据库连接已关闭。");
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 局限性

虽然 `DriverManager` 很简单易用，但在生产环境中有一些局限性：

1.  **性能问题**：每次 `getConnection()` 都会创建一个新的物理连接，创建连接的开销很大
2.  **缺乏连接管理**：没有连接池功能，连接无法复用
3.  **配置分散**：连接参数分散在代码中，难以统一管理

## 生产环境推荐：使用 DataSource

对于生产环境，推荐使用 `DataSource` 和连接池（如 HikariCP）：

```java
import com.zaxxer.hikari.HikariDataSource;
import javax.sql.DataSource;
import java.sql.Connection;

public class DataSourceExample {
    public static void main(String[] args) {
        HikariDataSource dataSource = new HikariDataSource();
        dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/mydb");
        dataSource.setUsername("root");
        dataSource.setPassword("1234");
        dataSource.setMaximumPoolSize(10); // 连接池大小
        
        try (Connection conn = dataSource.getConnection()) {
            System.out.println("从连接池获取连接成功！");
            // 使用连接...
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            dataSource.close(); // 关闭连接池
        }
    }
}
```

## 总结

| 特性         | DriverManager        | DataSource + 连接池  |
| ------------ | -------------------- | -------------------- |
| **连接创建** | 每次创建新连接       | 从池中获取/归还      |
| **性能**     | 较差（频繁创建连接） | 优秀（连接复用）     |
| **资源管理** | 无                   | 完善的连接管理       |
| **适用场景** | 简单应用、测试       | 生产环境、高并发应用 |
| **配置方式** | 代码中硬编码         | 外部配置文件         |

`DriverManager` 是学习 JDBC 和理解数据库连接原理的基础，但在实际企业级开发中，通常会使用 `DataSource` 和连接池来获得更好的性能和可维护性。



# Connection

`Connection` 是 `java.sql` 包中的一个**接口**，它代表与特定数据库的**会话**（session）。一个 `Connection` 对象就是一条通往数据库的"通信链路"，所有与数据库的交互都是通过这个连接进行的。

## 主要功能和方法

### 1. 创建SQL语句对象

```java
// 创建基本的 Statement 对象（容易SQL注入，不推荐用于用户输入）
Statement stmt = connection.createStatement();

// 创建预编译的 PreparedStatement（安全，推荐使用）
String sql = "SELECT * FROM users WHERE id = ?";
PreparedStatement pstmt = connection.prepareStatement(sql);

// 创建可滚动的 Statement（支持结果集前后移动）
Statement scrollStmt = connection.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE, 
    ResultSet.CONCUR_READ_ONLY
);

// 创建可更新的 Statement
Statement updateStmt = connection.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,
    ResultSet.CONCUR_UPDATABLE
);
```

### 2. 事务管理

```java
try {
    // 关闭自动提交，开启事务
    connection.setAutoCommit(false);
    
    // 执行多个数据库操作
    String sql1 = "UPDATE account SET balance = balance - 100 WHERE id = 1";
    String sql2 = "UPDATE account SET balance = balance + 100 WHERE id = 2";
    
    Statement stmt = connection.createStatement();
    stmt.executeUpdate(sql1);
    stmt.executeUpdate(sql2);
    
    // 提交事务
    connection.commit();
    System.out.println("转账成功！");
    
} catch (SQLException e) {
    try {
        // 回滚事务
        connection.rollback();
        System.out.println("事务回滚！");
    } catch (SQLException ex) {
        ex.printStackTrace();
    }
    e.printStackTrace();
} finally {
    try {
        // 恢复自动提交模式
        connection.setAutoCommit(true);
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```

### 3. 连接状态检查

```java
// 检查连接是否关闭
if (connection.isClosed()) {
    System.out.println("连接已关闭");
}

// 检查是否为只读模式
boolean isReadOnly = connection.isReadOnly();

// 检查自动提交状态
boolean autoCommit = connection.getAutoCommit();
```

### 4. 元数据获取

```java
// 获取数据库元数据
DatabaseMetaData metaData = connection.getMetaData();

System.out.println("数据库产品: " + metaData.getDatabaseProductName());
System.out.println("数据库版本: " + metaData.getDatabaseProductVersion());
System.out.println("驱动名称: " + metaData.getDriverName());
System.out.println("驱动版本: " + metaData.getDriverVersion());
System.out.println("JDBC版本: " + metaData.getJDBCMajorVersion() + "." + metaData.getJDBCMinorVersion());

// 获取数据库支持的功能
System.out.println("支持事务: " + metaData.supportsTransactions());
System.out.println("支持批量更新: " + metaData.supportsBatchUpdates());
```

## 完整的使用示例

```java
import java.sql.*;

public class ConnectionExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "123456";
        
        Connection connection = null;
        
        try {
            // 1. 建立连接
            connection = DriverManager.getConnection(url, user, password);
            
            // 2. 检查连接状态
            System.out.println("连接是否关闭: " + connection.isClosed());
            System.out.println("自动提交状态: " + connection.getAutoCommit());
            
            // 3. 获取数据库信息
            DatabaseMetaData metaData = connection.getMetaData();
            System.out.println("=== 数据库信息 ===");
            System.out.println("数据库: " + metaData.getDatabaseProductName());
            System.out.println("版本: " + metaData.getDatabaseProductVersion());
            System.out.println("URL: " + metaData.getURL());
            System.out.println("用户名: " + metaData.getUserName());
            
            // 4. 执行简单查询
            System.out.println("=== 执行查询 ===");
            try (Statement stmt = connection.createStatement();
                 ResultSet rs = stmt.executeQuery("SELECT NOW() as current_time")) {
                
                if (rs.next()) {
                    System.out.println("当前数据库时间: " + rs.getTimestamp("current_time"));
                }
            }
            
            // 5. 测试事务
            testTransaction(connection);
            
        } catch (SQLException e) {
            System.err.println("数据库操作失败: " + e.getMessage());
            e.printStackTrace();
        } finally {
            // 6. 关闭连接
            if (connection != null) {
                try {
                    connection.close();
                    System.out.println("连接已关闭");
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    
    // 事务测试方法
    private static void testTransaction(Connection conn) throws SQLException {
        try {
            // 开始事务
            conn.setAutoCommit(false);
            System.out.println("开始事务...");
            
            // 创建测试表
            try (Statement stmt = conn.createStatement()) {
                stmt.execute("CREATE TEMPORARY TABLE IF NOT EXISTS test_transaction (id INT, name VARCHAR(50))");
                stmt.execute("DELETE FROM test_transaction");
                
                // 插入数据
                stmt.executeUpdate("INSERT INTO test_transaction VALUES (1, '事务测试1')");
                stmt.executeUpdate("INSERT INTO test_transaction VALUES (2, '事务测试2')");
                
                System.out.println("插入2条记录");
            }
            
            // 查询数据
            try (Statement stmt = conn.createStatement();
                 ResultSet rs = stmt.executeQuery("SELECT COUNT(*) as count FROM test_transaction")) {
                
                if (rs.next()) {
                    System.out.println("当前记录数: " + rs.getInt("count"));
                }
            }
            
            // 提交事务
            conn.commit();
            System.out.println("事务提交成功");
            
        } catch (SQLException e) {
            // 回滚事务
            conn.rollback();
            System.out.println("事务回滚: " + e.getMessage());
            throw e;
        } finally {
            // 恢复自动提交
            conn.setAutoCommit(true);
        }
    }
}
```

## 连接池中的 Connection

在生产环境中，我们通常使用连接池来管理 Connection：

```java
import com.zaxxer.hikari.HikariDataSource;
import javax.sql.DataSource;
import java.sql.Connection;
import java.sql.SQLException;

public class ConnectionPoolExample {
    private static DataSource dataSource;
    
    static {
        HikariDataSource ds = new HikariDataSource();
        ds.setJdbcUrl("jdbc:mysql://localhost:3306/testdb");
        ds.setUsername("root");
        ds.setPassword("123456");
        ds.setMaximumPoolSize(10);
        ds.setMinimumIdle(2);
        ds.setConnectionTimeout(30000); // 30秒
        dataSource = ds;
    }
    
    public static Connection getConnection() throws SQLException {
        return dataSource.getConnection();
    }
    
    public static void main(String[] args) {
        try (Connection conn = getConnection()) {
            System.out.println("从连接池获取连接成功");
            System.out.println("连接是否来自连接池: " + !conn.isClosed());
            
            // 使用连接执行操作
            try (var stmt = conn.createStatement();
                 var rs = stmt.executeQuery("SELECT 1")) {
                if (rs.next()) {
                    System.out.println("测试查询成功: " + rs.getInt(1));
                }
            }
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## Connection 的重要特性

### 1. 自动提交 (Auto-commit)
- 默认情况下为 `true`
- 每个 SQL 语句都被视为一个事务并自动提交
- 对于需要多个操作的事务，需要设置为 `false`

### 2. 事务隔离级别
```java
// 获取当前隔离级别
int isolationLevel = connection.getTransactionIsolation();

// 设置隔离级别
connection.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);

// 常用隔离级别常量：
// Connection.TRANSACTION_READ_UNCOMMITTED
// Connection.TRANSACTION_READ_COMMITTED (最常用)
// Connection.TRANSACTION_REPEATABLE_READ
// Connection.TRANSACTION_SERIALIZABLE
```

### 3. 保存点 (Savepoints)
```java
connection.setAutoCommit(false);

Savepoint savepoint = connection.setSavepoint("SAVEPOINT_1");

try {
    // 执行一些操作
    // ...
    
    connection.releaseSavepoint(savepoint);
    connection.commit();
    
} catch (SQLException e) {
    connection.rollback(savepoint); // 回滚到保存点
    connection.commit();
}
```

## 最佳实践

1. **总是关闭连接**：使用 try-with-resources 确保连接关闭
2. **使用连接池**：生产环境一定要用连接池
3. **合理设置事务**：根据需要设置合适的事务隔离级别和自动提交
4. **避免长时间持有连接**：尽快完成操作并释放连接
5. **处理异常**：妥善处理 SQLException，确保事务正确回滚

`Connection` 是 JDBC 中最核心的接口之一，正确理解和使用它对于编写健壮的数据库应用程序至关重要。



# Statement

`Statement` 是 `java.sql` 包中的一个**接口**，用于执行静态的 SQL 语句并返回它产生的结果。它是执行 SQL 命令的**工作马**，通过 `Connection` 对象创建。

## Statement 的主要类型

| 类型                  | 接口                         | 特点                | 适用场景           |
| --------------------- | ---------------------------- | ------------------- | ------------------ |
| **Statement**         | `java.sql.Statement`         | 基本语句，易SQL注入 | 静态SQL，内部系统  |
| **PreparedStatement** | `java.sql.PreparedStatement` | 预编译，防SQL注入   | 动态参数，用户输入 |
| **CallableStatement** | `java.sql.CallableStatement` | 调用存储过程        | 执行数据库存储过程 |

## 基本 Statement 的使用

### 1. 创建 Statement

```java
Connection connection = DriverManager.getConnection(url, user, password);

// 创建基本 Statement
Statement statement = connection.createStatement();

// 创建可滚动、可更新的 Statement
Statement scrollStatement = connection.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,  // 可滚动
    ResultSet.CONCUR_READ_ONLY          // 只读
);

Statement updateStatement = connection.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,
    ResultSet.CONCUR_UPDATABLE          // 可更新
);
```

### 2. 执行 SQL 语句

```java
// 执行查询（返回 ResultSet）
String selectSql = "SELECT * FROM users";
ResultSet resultSet = statement.executeQuery(selectSql);

// 执行更新（返回受影响行数）
String insertSql = "INSERT INTO users (name, age) VALUES ('张三', 25)";
int insertCount = statement.executeUpdate(insertSql);
System.out.println("插入 " + insertCount + " 行");

String updateSql = "UPDATE users SET age = 26 WHERE name = '张三'";
int updateCount = statement.executeUpdate(updateSql);
System.out.println("更新 " + updateCount + " 行");

String deleteSql = "DELETE FROM users WHERE age < 18";
int deleteCount = statement.executeUpdate(deleteSql);
System.out.println("删除 " + deleteCount + " 行");

// 执行任意SQL（返回boolean，通常用于DDL）
String createSql = "CREATE TABLE IF NOT EXISTS products (id INT, name VARCHAR(100))";
boolean isResultSet = statement.execute(createSql);
```

### 3. 批量操作

```java
connection.setAutoCommit(false); // 关闭自动提交

Statement batchStatement = connection.createStatement();

// 添加批量操作
batchStatement.addBatch("INSERT INTO users (name, age) VALUES ('李四', 30)");
batchStatement.addBatch("UPDATE users SET age = 31 WHERE name = '李四'");
batchStatement.addBatch("DELETE FROM users WHERE age > 100");

// 执行批量操作
int[] results = batchStatement.executeBatch();
System.out.println("批量操作结果: " + Arrays.toString(results));

connection.commit(); // 提交事务
batchStatement.clearBatch(); // 清空批量
```

## 完整示例

```java
import java.sql.*;
import java.util.Arrays;

public class StatementExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "123456";
        
        try (Connection connection = DriverManager.getConnection(url, user, password);
             Statement statement = connection.createStatement()) {
            
            System.out.println("=== Statement 示例 ===");
            
            // 1. 创建测试表
            createTestTable(statement);
            
            // 2. 插入数据
            insertData(statement);
            
            // 3. 查询数据
            queryData(statement);
            
            // 4. 更新数据
            updateData(statement);
            
            // 5. 批量操作
            batchOperations(connection);
            
            // 6. 删除表（清理）
            statement.execute("DROP TABLE IF EXISTS employees");
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    private static void createTestTable(Statement stmt) throws SQLException {
        String createSql = "CREATE TABLE IF NOT EXISTS employees (" +
                          "id INT PRIMARY KEY AUTO_INCREMENT, " +
                          "name VARCHAR(50) NOT NULL, " +
                          "age INT, " +
                          "department VARCHAR(50), " +
                          "salary DECIMAL(10, 2)" +
                          ")";
        stmt.execute(createSql);
        System.out.println("创建表成功");
    }
    
    private static void insertData(Statement stmt) throws SQLException {
        String[] insertSqls = {
            "INSERT INTO employees (name, age, department, salary) VALUES ('张三', 25, '技术部', 8000.00)",
            "INSERT INTO employees (name, age, department, salary) VALUES ('李四', 30, '销售部', 12000.00)",
            "INSERT INTO employees (name, age, department, salary) VALUES ('王五', 28, '技术部', 9500.00)",
            "INSERT INTO employees (name, age, department, salary) VALUES ('赵六', 35, '人事部', 7000.00)"
        };
        
        for (String sql : insertSqls) {
            int count = stmt.executeUpdate(sql);
            System.out.println("插入 " + count + " 行: " + sql);
        }
    }
    
    private static void queryData(Statement stmt) throws SQLException {
        System.out.println("\n=== 查询所有员工 ===");
        String selectSql = "SELECT * FROM employees";
        try (ResultSet rs = stmt.executeQuery(selectSql)) {
            while (rs.next()) {
                System.out.printf("ID: %d, 姓名: %s, 年龄: %d, 部门: %s, 薪资: %.2f%n",
                                 rs.getInt("id"),
                                 rs.getString("name"),
                                 rs.getInt("age"),
                                 rs.getString("department"),
                                 rs.getDouble("salary"));
            }
        }
        
        System.out.println("\n=== 查询技术部员工 ===");
        String deptSql = "SELECT name, salary FROM employees WHERE department = '技术部'";
        try (ResultSet rs = stmt.executeQuery(deptSql)) {
            while (rs.next()) {
                System.out.printf("姓名: %s, 薪资: %.2f%n",
                                 rs.getString("name"),
                                 rs.getDouble("salary"));
            }
        }
    }
    
    private static void updateData(Statement stmt) throws SQLException {
        System.out.println("\n=== 更新数据 ===");
        String updateSql = "UPDATE employees SET salary = salary * 1.1 WHERE department = '技术部'";
        int updatedCount = stmt.executeUpdate(updateSql);
        System.out.println("为技术部员工加薪10%，影响 " + updatedCount + " 人");
        
        // 验证更新结果
        String verifySql = "SELECT name, salary FROM employees WHERE department = '技术部'";
        try (ResultSet rs = stmt.executeQuery(verifySql)) {
            while (rs.next()) {
                System.out.printf("姓名: %s, 新薪资: %.2f%n",
                                 rs.getString("name"),
                                 rs.getDouble("salary"));
            }
        }
    }
    
    private static void batchOperations(Connection conn) throws SQLException {
        System.out.println("\n=== 批量操作 ===");
        
        try (Statement batchStmt = conn.createStatement()) {
            conn.setAutoCommit(false); // 开始事务
            
            // 添加批量操作
            batchStmt.addBatch("INSERT INTO employees (name, age, department) VALUES ('孙七', 27, '财务部')");
            batchStmt.addBatch("UPDATE employees SET salary = 8500 WHERE name = '孙七'");
            batchStmt.addBatch("DELETE FROM employees WHERE age > 40");
            
            // 执行批量
            int[] results = batchStmt.executeBatch();
            System.out.println("批量操作结果: " + Arrays.toString(results));
            
            conn.commit(); // 提交事务
            System.out.println("批量操作提交成功");
            
        } catch (SQLException e) {
            conn.rollback(); // 回滚事务
            System.out.println("批量操作失败，已回滚");
            throw e;
        } finally {
            conn.setAutoCommit(true); // 恢复自动提交
        }
    }
}
```

## Statement 的重要方法

### 执行方法

```java
// 执行查询，返回ResultSet
ResultSet executeQuery(String sql) throws SQLException;

// 执行更新，返回受影响行数
int executeUpdate(String sql) throws SQLException;

// 执行任意SQL，返回boolean（true表示有ResultSet）
boolean execute(String sql) throws SQLException;
```

### 批量处理方法

```java
// 添加批量操作
void addBatch(String sql) throws SQLException;

// 执行批量操作
int[] executeBatch() throws SQLException;

// 清空批量操作
void clearBatch() throws SQLException;
```

### 结果集控制方法

```java
// 获取生成的主键
ResultSet getGeneratedKeys() throws SQLException;

// 设置获取的最大行数
void setMaxRows(int max) throws SQLException;

// 设置查询超时时间（秒）
void setQueryTimeout(int seconds) throws SQLException;

// 设置每次从数据库获取的行数（用于大数据量）
void setFetchSize(int rows) throws SQLException;
```

## Statement 的局限性

### SQL 注入风险（严重安全问题）

**错误示例（易受攻击）：**
```java
// 危险！容易SQL注入
String userInput = "'; DROP TABLE users; --";
String sql = "SELECT * FROM users WHERE name = '" + userInput + "'";
ResultSet rs = statement.executeQuery(sql);
```

**正确做法：使用 PreparedStatement**
```java
String userInput = "'; DROP TABLE users; --";
String sql = "SELECT * FROM users WHERE name = ?";
PreparedStatement pstmt = connection.prepareStatement(sql);
pstmt.setString(1, userInput); // 安全，参数会被正确处理
ResultSet rs = pstmt.executeQuery();
```

### 性能问题

- 每次执行都需要编译 SQL
- 无法利用数据库的预编译功能
- 对于重复执行的SQL效率低下

## 最佳实践

1. **优先使用 PreparedStatement**：防止SQL注入，提高性能
2. **及时关闭 Statement**：使用 try-with-resources
3. **合理使用批量操作**：大量数据操作时使用批量
4. **设置合适的超时时间**：避免长时间阻塞
5. **避免字符串拼接SQL**：永远不要用字符串拼接用户输入

## 使用场景

### 适合使用 Statement：
- 执行 DDL 语句（CREATE, DROP, ALTER）
- 执行静态的、内部使用的 SQL
- 简单的管理脚本

### 不适合使用 Statement：
- 包含用户输入的 SQL
- 需要重复执行的 SQL
- 生产环境的业务代码

虽然 `Statement` 简单易用，但在实际开发中应该优先考虑使用 `PreparedStatement` 来保证安全性和性能。



# ResultSet

`ResultSet` 是 `java.sql` 包中的一个**接口**，它表示数据库查询结果的数据表。你可以把它想象成一个**指向数据的游标**，最初定位在第一行之前，通过 `next()` 方法逐行移动来访问数据。

## ResultSet 的主要特性

### 1. 类型（Type）

```java
// 不可滚动（只能向前）
ResultSet.TYPE_FORWARD_ONLY

// 可滚动，不敏感（数据库变化不可见）
ResultSet.TYPE_SCROLL_INSENSITIVE

// 可滚动，敏感（数据库变化可见）
ResultSet.TYPE_SCROLL_SENSITIVE
```

### 2. 并发性（Concurrency）

```java
// 只读
ResultSet.CONCUR_READ_ONLY

// 可更新
ResultSet.CONCUR_UPDATABLE
```

## 创建 ResultSet

```java
Statement stmt = connection.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE,
    ResultSet.CONCUR_READ_ONLY
);

String sql = "SELECT id, name, age, salary FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

## 遍历和读取数据

### 基本遍历

```java
// 最基本的遍历方式
while (rs.next()) {
    int id = rs.getInt("id");
    String name = rs.getString("name");
    int age = rs.getInt("age");
    double salary = rs.getDouble("salary");
    
    System.out.printf("ID: %d, 姓名: %s, 年龄: %d, 薪资: %.2f%n", 
                     id, name, age, salary);
}
```

### 可滚动 ResultSet 的遍历

```java
// 移动到第一行
rs.first();
System.out.println("第一行: " + rs.getString("name"));

// 移动到最后一行
rs.last();
System.out.println("最后一行: " + rs.getString("name"));

// 移动到第3行
rs.absolute(3);
System.out.println("第3行: " + rs.getString("name"));

// 向前移动一行
rs.previous();
System.out.println("第2行: " + rs.getString("name"));

// 相对移动（从当前位置移动2行）
rs.relative(2);
System.out.println("第4行: " + rs.getString("name"));

// 回到第一行之前
rs.beforeFirst();
```

## 完整示例

```java
import java.sql.*;
import java.math.BigDecimal;

public class ResultSetExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "123456";
        
        try (Connection connection = DriverManager.getConnection(url, user, password);
             Statement stmt = connection.createStatement(
                 ResultSet.TYPE_SCROLL_INSENSITIVE,
                 ResultSet.CONCUR_READ_ONLY
             )) {
            
            System.out.println("=== ResultSet 示例 ===");
            
            // 创建测试数据
            createTestData(stmt);
            
            // 1. 基本查询和遍历
            basicQuery(stmt);
            
            // 2. 可滚动 ResultSet
            scrollableResultSet(stmt);
            
            // 3. 元数据信息
            resultSetMetadata(stmt);
            
            // 4. 可更新 ResultSet
            updatableResultSet(connection);
            
            // 清理
            stmt.execute("DROP TABLE IF EXISTS products");
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    private static void createTestData(Statement stmt) throws SQLException {
        stmt.execute("CREATE TABLE IF NOT EXISTS products (" +
                    "id INT PRIMARY KEY AUTO_INCREMENT, " +
                    "name VARCHAR(100) NOT NULL, " +
                    "category VARCHAR(50), " +
                    "price DECIMAL(10, 2), " +
                    "stock INT, " +
                    "created_date DATE" +
                    ")");
        
        stmt.execute("DELETE FROM products");
        
        String[] inserts = {
            "INSERT INTO products (name, category, price, stock, created_date) VALUES " +
            "('iPhone 13', '电子产品', 5999.00, 100, '2023-01-15')",
            "INSERT INTO products (name, category, price, stock, created_date) VALUES " +
            "('MacBook Pro', '电子产品', 12999.00, 50, '2023-02-20')",
            "INSERT INTO products (name, category, price, stock, created_date) VALUES " +
            "('咖啡机', '家电', 899.00, 30, '2023-03-10')",
            "INSERT INTO products (name, category, price, stock, created_date) VALUES " +
            "('办公椅', '家具', 499.00, 80, '2023-04-05')",
            "INSERT INTO products (name, category, price, stock, created_date) VALUES " +
            "('篮球', '体育用品', 199.00, 120, '2023-05-12')"
        };
        
        for (String sql : inserts) {
            stmt.executeUpdate(sql);
        }
        System.out.println("测试数据创建完成");
    }
    
    private static void basicQuery(Statement stmt) throws SQLException {
        System.out.println("\n=== 基本查询 ===");
        
        String sql = "SELECT id, name, category, price, stock, created_date FROM products";
        try (ResultSet rs = stmt.executeQuery(sql)) {
            
            System.out.printf("%-3s %-15s %-10s %-8s %-5s %-12s%n", 
                            "ID", "名称", "分类", "价格", "库存", "创建日期");
            System.out.println("------------------------------------------------------------");
            
            while (rs.next()) {
                int id = rs.getInt("id");
                String name = rs.getString("name");
                String category = rs.getString("category");
                BigDecimal price = rs.getBigDecimal("price");
                int stock = rs.getInt("stock");
                Date createdDate = rs.getDate("created_date");
                
                System.out.printf("%-3d %-15s %-10s %-8.2f %-5d %-12s%n",
                                id, name, category, price, stock, createdDate);
            }
        }
    }
    
    private static void scrollableResultSet(Statement stmt) throws SQLException {
        System.out.println("\n=== 可滚动 ResultSet ===");
        
        String sql = "SELECT id, name, price FROM products ORDER BY price DESC";
        try (ResultSet rs = stmt.executeQuery(sql)) {
            
            // 移动到最后一行的下一行，获取总行数
            rs.last();
            int rowCount = rs.getRow();
            System.out.println("总记录数: " + rowCount);
            
            // 回到第一行之前
            rs.beforeFirst();
            
            System.out.println("\n最贵的3个产品:");
            int count = 0;
            while (rs.next() && count < 3) {
                System.out.printf("第%d名: %s (¥%.2f)%n",
                                rs.getRow(),
                                rs.getString("name"),
                                rs.getBigDecimal("price"));
                count++;
            }
            
            // 直接跳到第5行
            if (rs.absolute(5)) {
                System.out.println("\n第5行数据: " + rs.getString("name"));
            }
            
            // 向前移动2行
            if (rs.relative(-2)) {
                System.out.println("向前移动2行: " + rs.getString("name"));
            }
        }
    }
    
    private static void resultSetMetadata(Statement stmt) throws SQLException {
        System.out.println("\n=== ResultSet 元数据 ===");
        
        String sql = "SELECT * FROM products";
        try (ResultSet rs = stmt.executeQuery(sql)) {
            ResultSetMetaData metaData = rs.getMetaData();
            
            int columnCount = metaData.getColumnCount();
            System.out.println("列数: " + columnCount);
            System.out.println("\n列信息:");
            System.out.printf("%-15s %-15s %-10s %-5s%n", "列名", "类型", "大小", "可空");
            System.out.println("------------------------------------------------");
            
            for (int i = 1; i <= columnCount; i++) {
                String columnName = metaData.getColumnName(i);
                String columnType = metaData.getColumnTypeName(i);
                int columnSize = metaData.getPrecision(i);
                boolean isNullable = metaData.isNullable(i) == ResultSetMetaData.columnNullable;
                
                System.out.printf("%-15s %-15s %-10d %-5s%n",
                                columnName, columnType, columnSize, isNullable ? "是" : "否");
            }
        }
    }
    
    private static void updatableResultSet(Connection conn) throws SQLException {
        System.out.println("\n=== 可更新 ResultSet ===");
        
        // 创建可更新的 Statement
        try (Statement stmt = conn.createStatement(
                ResultSet.TYPE_SCROLL_INSENSITIVE,
                ResultSet.CONCUR_UPDATABLE);
             ResultSet rs = stmt.executeQuery("SELECT id, name, price, stock FROM products WHERE category = '电子产品'")) {
            
            System.out.println("更新前的电子产品:");
            while (rs.next()) {
                System.out.printf("ID: %d, 名称: %s, 价格: %.2f, 库存: %d%n",
                                rs.getInt("id"),
                                rs.getString("name"),
                                rs.getBigDecimal("price"),
                                rs.getInt("stock"));
            }
            
            // 更新数据 - 回到第一行
            rs.beforeFirst();
            while (rs.next()) {
                // 涨价10%
                BigDecimal currentPrice = rs.getBigDecimal("price");
                BigDecimal newPrice = currentPrice.multiply(new BigDecimal("1.1"));
                rs.updateBigDecimal("price", newPrice);
                
                // 库存增加20
                int currentStock = rs.getInt("stock");
                rs.updateInt("stock", currentStock + 20);
                
                // 提交更新到数据库
                rs.updateRow();
            }
            
            System.out.println("\n更新后的电子产品:");
            rs.beforeFirst();
            while (rs.next()) {
                System.out.printf("ID: %d, 名称: %s, 新价格: %.2f, 新库存: %d%n",
                                rs.getInt("id"),
                                rs.getString("name"),
                                rs.getBigDecimal("price"),
                                rs.getInt("stock"));
            }
        }
    }
}
```

## ResultSet 的重要方法

### 1. 游标移动方法

```java
boolean next() throws SQLException;          // 移动到下一行
boolean previous() throws SQLException;      // 移动到上一行
boolean first() throws SQLException;         // 移动到第一行
boolean last() throws SQLException;          // 移动到最后一行
boolean absolute(int row) throws SQLException; // 移动到指定行
boolean relative(int rows) throws SQLException; // 相对移动
void beforeFirst() throws SQLException;      // 移动到第一行之前
void afterLast() throws SQLException;        // 移动到最后一行之后
boolean isFirst() throws SQLException;       // 是否在第一行
boolean isLast() throws SQLException;        // 是否在最后一行
```

### 2. 数据获取方法

```java
// 按列名获取
String getString(String columnLabel) throws SQLException;
int getInt(String columnLabel) throws SQLException;
double getDouble(String columnLabel) throws SQLException;
Date getDate(String columnLabel) throws SQLException;
BigDecimal getBigDecimal(String columnLabel) throws SQLException;

// 按列索引获取（从1开始）
String getString(int columnIndex) throws SQLException;
int getInt(int columnIndex) throws SQLException;

// 获取元数据
ResultSetMetaData getMetaData() throws SQLException;
```

### 3. 可更新 ResultSet 方法

```java
// 更新数据
void updateString(String columnLabel, String x) throws SQLException;
void updateInt(String columnLabel, int x) throws SQLException;
void updateRow() throws SQLException; // 提交更新

// 插入新行
void moveToInsertRow() throws SQLException;
void insertRow() throws SQLException;

// 删除行
void deleteRow() throws SQLException;

// 取消更新
void cancelRowUpdates() throws SQLException;
```

## 最佳实践

1. **总是关闭 ResultSet**：使用 try-with-resources
2. **按需获取数据**：只获取需要的列，避免 `SELECT *`
3. **使用正确的数据类型**：`getString()` 用于文本，`getInt()` 用于整数等
4. **处理 NULL 值**：使用 `wasNull()` 检查前一个获取的值是否为 NULL
5. **使用批量读取**：对于大数据集，设置合适的 fetchSize

```java
// NULL 值处理示例
String name = rs.getString("name");
if (rs.wasNull()) {
    name = "未知";
}

// 设置获取大小
stmt.setFetchSize(100);
```

## 常见使用模式

### 1. 简单遍历
```java
while (rs.next()) {
    // 处理每一行数据
}
```

### 2. 检查是否存在数据
```java
if (rs.next()) {
    // 有数据
} else {
    // 无数据
}
```

### 3. 获取单值
```java
String sql = "SELECT COUNT(*) FROM users";
ResultSet rs = stmt.executeQuery(sql);
if (rs.next()) {
    int count = rs.getInt(1);
    System.out.println("用户总数: " + count);
}
```

`ResultSet` 是处理数据库查询结果的核心接口，熟练掌握它的各种用法对于编写高效的数据库应用程序至关重要。

好的，我们来深入解析 JDBC 中非常重要的 `PreparedStatement` 接口。

# PreparedStatement

`PreparedStatement` 是 `Statement` 的子接口，它表示**预编译的 SQL 语句**。与普通的 `Statement` 不同，`PreparedStatement` 使用**参数占位符** (`?`) 来代替具体的值，然后在执行前设置这些参数的值。

## 为什么使用 PreparedStatement？

1. **防止 SQL 注入攻击**（最主要优势）

2. **提高性能**（预编译，可重复使用）

3. **更好的代码可读性和维护性**

4. **自动处理特殊字符**

## 基本用法

### 创建 PreparedStatement

```java
String sql = "INSERT INTO users (name, email, age) VALUES (?, ?, ?)";
PreparedStatement pstmt = connection.prepareStatement(sql);
```

### 设置参数值

```java
// 设置参数（索引从1开始）
pstmt.setString(1, "张三");     // 第一个问号
pstmt.setString(2, "zhangsan@example.com"); // 第二个问号
pstmt.setInt(3, 25);           // 第三个问号

// 执行更新
int rowsAffected = pstmt.executeUpdate();
```

## 完整示例

```java
import java.sql.*;
import java.math.BigDecimal;

public class PreparedStatementExample {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/testdb";
        String user = "root";
        String password = "123456";
        
        try (Connection connection = DriverManager.getConnection(url, user, password)) {
            
            System.out.println("=== PreparedStatement 示例 ===");
            
            // 创建测试表
            createTable(connection);
            
            // 1. 插入数据
            insertData(connection);
            
            // 2. 查询数据
            queryData(connection);
            
            // 3. 更新数据
            updateData(connection);
            
            // 4. 防止SQL注入演示
            demonstrateSqlInjectionProtection(connection);
            
            // 5. 批量操作
            batchOperations(connection);
            
            // 6. 获取生成的主键
            getGeneratedKeys(connection);
            
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    
    private static void createTable(Connection conn) throws SQLException {
        String sql = "CREATE TABLE IF NOT EXISTS employees (" +
                    "id INT PRIMARY KEY AUTO_INCREMENT, " +
                    "name VARCHAR(50) NOT NULL, " +
                    "email VARCHAR(100) UNIQUE, " +
                    "age INT, " +
                    "salary DECIMAL(10, 2), " +
                    "department VARCHAR(50), " +
                    "hire_date DATE" +
                    ")";
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.execute();
            System.out.println("表创建成功");
        }
    }
    
    private static void insertData(Connection conn) throws SQLException {
        String sql = "INSERT INTO employees (name, email, age, salary, department, hire_date) " +
                    "VALUES (?, ?, ?, ?, ?, ?)";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            
            // 插入第一条记录
            pstmt.setString(1, "张三");
            pstmt.setString(2, "zhangsan@example.com");
            pstmt.setInt(3, 25);
            pstmt.setBigDecimal(4, new BigDecimal("8000.00"));
            pstmt.setString(5, "技术部");
            pstmt.setDate(6, Date.valueOf("2023-01-15"));
            pstmt.executeUpdate();
            
            // 插入第二条记录（重用同一个PreparedStatement）
            pstmt.setString(1, "李四");
            pstmt.setString(2, "lisi@example.com");
            pstmt.setInt(3, 30);
            pstmt.setBigDecimal(4, new BigDecimal("12000.00"));
            pstmt.setString(5, "销售部");
            pstmt.setDate(6, Date.valueOf("2022-08-20"));
            pstmt.executeUpdate();
            
            // 插入第三条记录
            pstmt.setString(1, "王五");
            pstmt.setString(2, "wangwu@example.com");
            pstmt.setInt(3, 28);
            pstmt.setBigDecimal(4, new BigDecimal("9500.00"));
            pstmt.setString(5, "技术部");
            pstmt.setDate(6, Date.valueOf("2023-03-10"));
            pstmt.executeUpdate();
            
            System.out.println("插入3条记录成功");
        }
    }
    
    private static void queryData(Connection conn) throws SQLException {
        System.out.println("\n=== 查询示例 ===");
        
        // 查询技术部员工
        String sql = "SELECT id, name, age, salary, hire_date FROM employees WHERE department = ?";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setString(1, "技术部");
            
            try (ResultSet rs = pstmt.executeQuery()) {
                System.out.println("技术部员工列表:");
                System.out.printf("%-3s %-10s %-4s %-8s %-12s%n", 
                                "ID", "姓名", "年龄", "薪资", "入职日期");
                System.out.println("------------------------------------------");
                
                while (rs.next()) {
                    System.out.printf("%-3d %-10s %-4d %-8.2f %-12s%n",
                                    rs.getInt("id"),
                                    rs.getString("name"),
                                    rs.getInt("age"),
                                    rs.getBigDecimal("salary"),
                                    rs.getDate("hire_date"));
                }
            }
        }
        
        // 查询薪资范围内的员工
        System.out.println("\n薪资在9000-13000之间的员工:");
        String salarySql = "SELECT name, salary, department FROM employees WHERE salary BETWEEN ? AND ?";
        
        try (PreparedStatement pstmt = conn.prepareStatement(salarySql)) {
            pstmt.setBigDecimal(1, new BigDecimal("9000.00"));
            pstmt.setBigDecimal(2, new BigDecimal("13000.00"));
            
            try (ResultSet rs = pstmt.executeQuery()) {
                while (rs.next()) {
                    System.out.printf("姓名: %s, 薪资: %.2f, 部门: %s%n",
                                    rs.getString("name"),
                                    rs.getBigDecimal("salary"),
                                    rs.getString("department"));
                }
            }
        }
    }
    
    private static void updateData(Connection conn) throws SQLException {
        System.out.println("\n=== 更新示例 ===");
        
        // 为技术部员工加薪10%
        String sql = "UPDATE employees SET salary = salary * ? WHERE department = ?";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setBigDecimal(1, new BigDecimal("1.10")); // 加薪10%
            pstmt.setString(2, "技术部");
            
            int rowsUpdated = pstmt.executeUpdate();
            System.out.println("更新了 " + rowsUpdated + " 条记录");
            
            // 验证更新结果
            String verifySql = "SELECT name, salary FROM employees WHERE department = ?";
            try (PreparedStatement verifyStmt = conn.prepareStatement(verifySql)) {
                verifyStmt.setString(1, "技术部");
                
                try (ResultSet rs = verifyStmt.executeQuery()) {
                    System.out.println("更新后的薪资:");
                    while (rs.next()) {
                        System.out.printf("姓名: %s, 新薪资: %.2f%n",
                                        rs.getString("name"),
                                        rs.getBigDecimal("salary"));
                    }
                }
            }
        }
    }
    
    private static void demonstrateSqlInjectionProtection(Connection conn) throws SQLException {
        System.out.println("\n=== SQL注入防护演示 ===");
        
        // 模拟用户输入（恶意输入）
        String maliciousInput = "'; DROP TABLE employees; --";
        
        // 使用 Statement（危险！）
        System.out.println("使用 Statement（危险）:");
        String unsafeSql = "SELECT * FROM employees WHERE name = '" + maliciousInput + "'";
        try (Statement stmt = conn.createStatement()) {
            ResultSet rs = stmt.executeQuery(unsafeSql);
            System.out.println("查询完成（如果表被删除，这里会报错）");
        }
        
        // 使用 PreparedStatement（安全）
        System.out.println("使用 PreparedStatement（安全）:");
        String safeSql = "SELECT * FROM employees WHERE name = ?";
        try (PreparedStatement pstmt = conn.prepareStatement(safeSql)) {
            pstmt.setString(1, maliciousInput);
            
            try (ResultSet rs = pstmt.executeQuery()) {
                if (!rs.next()) {
                    System.out.println("没有找到匹配的记录（安全）");
                }
            }
        }
    }
    
    private static void batchOperations(Connection conn) throws SQLException {
        System.out.println("\n=== 批量操作示例 ===");
        
        String sql = "INSERT INTO employees (name, email, age, salary, department) VALUES (?, ?, ?, ?, ?)";
        
        try (PreparedStatement pstmt = conn.prepareStatement(sql)) {
            
            // 添加批量操作
            addBatchEmployee(pstmt, "赵六", "zhaoliu@example.com", 35, new BigDecimal("7000.00"), "人事部");
            addBatchEmployee(pstmt, "孙七", "sunqi@example.com", 27, new BigDecimal("8500.00"), "财务部");
            addBatchEmployee(pstmt, "周八", "zhouba@example.com", 32, new BigDecimal("11000.00"), "销售部");
            
            // 执行批量操作
            int[] results = pstmt.executeBatch();
            System.out.println("批量插入完成，影响行数: " + results.length);
            
            // 清空批量
            pstmt.clearBatch();
        }
    }
    
    private static void addBatchEmployee(PreparedStatement pstmt, String name, String email, 
                                       int age, BigDecimal salary, String department) throws SQLException {
        pstmt.setString(1, name);
        pstmt.setString(2, email);
        pstmt.setInt(3, age);
        pstmt.setBigDecimal(4, salary);
        pstmt.setString(5, department);
        pstmt.addBatch();
    }
    
    private static void getGeneratedKeys(Connection conn) throws SQLException {
        System.out.println("\n=== 获取自增主键示例 ===");
        
        String sql = "INSERT INTO employees (name, email, age, department) VALUES (?, ?, ?, ?)";
        
        // 指定需要返回生成的主键
        try (PreparedStatement pstmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)) {
            pstmt.setString(1, "吴九");
            pstmt.setString(2, "wujiu@example.com");
            pstmt.setInt(3, 29);
            pstmt.setString(4, "市场部");
            
            int rowsAffected = pstmt.executeUpdate();
            System.out.println("插入 " + rowsAffected + " 行");
            
            // 获取生成的主键
            try (ResultSet generatedKeys = pstmt.getGeneratedKeys()) {
                if (generatedKeys.next()) {
                    long newId = generatedKeys.getLong(1);
                    System.out.println("新插入记录的ID: " + newId);
                }
            }
        }
    }
}
```

## PreparedStatement 的重要方法

### 1. 参数设置方法

```java
// 设置各种类型的参数
void setString(int parameterIndex, String x) throws SQLException;
void setInt(int parameterIndex, int x) throws SQLException;
void setDouble(int parameterIndex, double x) throws SQLException;
void setBoolean(int parameterIndex, boolean x) throws SQLException;
void setDate(int parameterIndex, Date x) throws SQLException;
void setTimestamp(int parameterIndex, Timestamp x) throws SQLException;
void setBigDecimal(int parameterIndex, BigDecimal x) throws SQLException;
void setNull(int parameterIndex, int sqlType) throws SQLException;

// 设置对象（自动类型转换）
void setObject(int parameterIndex, Object x) throws SQLException;
void setObject(int parameterIndex, Object x, int targetSqlType) throws SQLException;
```

### 2. 批量操作方法

```java
void addBatch() throws SQLException;      // 添加当前参数到批量
void clearParameters() throws SQLException; // 清除所有参数
```

### 3. 元数据方法

```java
ParameterMetaData getParameterMetaData() throws SQLException;
```

## 参数数据类型对照表

| Java 类型    | PreparedStatement 方法 | SQL 类型                  |
| ------------ | ---------------------- | ------------------------- |
| `String`     | `setString()`          | `VARCHAR`, `CHAR`, `TEXT` |
| `int`        | `setInt()`             | `INTEGER`, `INT`          |
| `long`       | `setLong()`            | `BIGINT`                  |
| `double`     | `setDouble()`          | `DOUBLE`, `FLOAT`         |
| `boolean`    | `setBoolean()`         | `BOOLEAN`, `BIT`          |
| `Date`       | `setDate()`            | `DATE`                    |
| `Time`       | `setTime()`            | `TIME`                    |
| `Timestamp`  | `setTimestamp()`       | `TIMESTAMP`, `DATETIME`   |
| `BigDecimal` | `setBigDecimal()`      | `DECIMAL`, `NUMERIC`      |
| `byte[]`     | `setBytes()`           | `BLOB`, `BINARY`          |

## 最佳实践

1. **总是使用 PreparedStatement**：代替普通的 Statement
2. **正确设置参数类型**：使用匹配的数据类型方法
3. **重用 PreparedStatement**：对于重复执行的SQL
4. **使用批量操作**：大量数据插入时
5. **及时关闭资源**：使用 try-with-resources
6. **处理 NULL 值**：使用 `setNull()` 方法

```java
// NULL 值处理示例
if (email == null) {
    pstmt.setNull(2, Types.VARCHAR);
} else {
    pstmt.setString(2, email);
}
```

## 性能优势

```java
// 重复使用同一个 PreparedStatement（高性能）
String sql = "UPDATE products SET price = ? WHERE id = ?";
try (PreparedStatement pstmt = connection.prepareStatement(sql)) {
    
    for (Product product : products) {
        pstmt.setBigDecimal(1, product.getPrice());
        pstmt.setInt(2, product.getId());
        pstmt.executeUpdate();
    }
}
```

`PreparedStatement` 是 JDBC 编程中**必须掌握**的核心接口，它提供了安全性、性能和代码可读性方面的巨大优势。在生产环境的代码中，应该始终优先使用 `PreparedStatement` 而不是普通的 `Statement`。









