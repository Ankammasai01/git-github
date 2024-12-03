# jdbc connection
package jdbc;
import java.sql.*;
public class demo {

	    public static void main(String[] args) {
	        // Database credentials
	        String url = "jdbc:mysql://127.0.0.1:3306/payment?useSSL=false"; // Corrected URL format
	        String user_name = "root";
	        String password = "Ankammasai@01";
	        String query = "SELECT customer_payment, COUNT(customer_name) AS name_count " +
                    "FROM pay GROUP BY customer_payment ORDER BY customer_payment";
	        		 // Ensure table 'hi' exists in the database

	        // Using try-with-resources for automatic resource management
	        try (
	            // Establishing connection
	            Connection con = DriverManager.getConnection(url, user_name, password);

	            // Creating statement object
	            Statement st = con.createStatement();

	            // Executing query
	            ResultSet rs = st.executeQuery(query)
	        ) {
	            // Processing result
	            while (rs.next()) { // Loop through rows
	                String customerPayment = rs.getString("customer_payment"); // Replace 'column_name' with an actual column name
	               int namecount=rs.getInt("name_count");

	               System.out.println(customerPayment + " | " + namecount);
	            }
	        } catch (SQLException e) {
	            // Handling SQL errors
	            System.out.println("SQL Exception: " + e.getMessage());
	            e.printStackTrace();
	        } catch (Exception e) {
	            // Handling other errors
	            System.out.println("Exception: " + e.getMessage());
	            e.printStackTrace();
	        }
	    }
	}
