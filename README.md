# Library-Management
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Date;
import java.util.Scanner;
import java.sql.PreparedStatement;
import javax.swing.*; 
public class App {
  public static Scanner sc = new Scanner(System.in);
    public static void main(String[] args) throws Exception { 
   Connection conn = null;
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
   String url = "jdbc:mysql://localhost/bharti_womens_lib";
            String user = "root";
            String password = "TheMFRS";
            conn = DriverManager.getConnection(url, user, password);
            while(true){
                System.out.print("\033[H\033[2J"); 
                System.out.flush();
                System.out.println("----- Library Management System -----");
                System.out.println("\nEnter\n\t1. Add Book \n\t2. Add Student Member \n\t3. Borrow Book \n\t4. Return Book \n\t5. List Books \n\t6. Update Book \n\t7. Update Student \n\t8. Delete Book \n\t9. Delete Student \n\t0. Exit \n");
                System.out.print("Press : ");
 int choice = sc.nextInt();
                switch (choice) {
                    case 1 -> insertBook(conn);
                    case 2 -> insertStudent(conn);
                    case 3 -> assignBook(conn);
                    case 4 -> submitBook(conn);
                    case 5 -> listBooks(conn);
                    case 6 -> listStudents(conn);
                    case 7 -> updateBook(conn);
                    case 8 -> updateStudent(conn);
                    case 9 -> deleteBook(conn);
                    case 10 -> deleteStudent(conn);
                    case 11 -> getBook(conn);
                    case 12 -> getStudent(conn);
                    case 0 -> exit(conn);
                    default -> System.out.println("Invalid Choice!");
                }
            } 
        } catch (ClassNotFoundException | SQLException ex) {
            ex.printStackTrace();
   public static void insertBook(Connection conn)
    {
        System.out.print("\033[H\033[2J"); 
        System.out.flush();
        System.out.println("\n\n----- Add New Book -----\n\n");
        System.out.println("Enter Book Details:");
        PreparedStatement pstmt = null;
        // String sql= "insert into book(id, title, author, publication, edition, pub_year) value(?, ?, ?, ?, ?, ?)";
        String sql = "insert into book(id, title, author, publication, edition, pub_year, student_id, issuedate, stat) values (?, ?, ?, ?, ?, ?, ?, ?, ?)";

public static void insertStudent(Connection conn)
    {
        System.out.print("\033[H\033[2J"); // ANSI escape code to clear the screen
        System.out.flush();
        System.out.println("\n\n----- Add New Student Member -----\n\n");
        System.out.println("Enter Student Details:");
  PreparedStatement pstmt = null;
        String sql= "insert into student(rollno, s_name, class, division, contact) value(?, ?, ?, ?, ?)";
try {
            pstmt = conn.prepareStatement(sql, pstmt.RETURN_GENERATED_KEYS);
sc.nextLine();
            System.out.print("\tRollno: ");
            String Rollno= sc.nextLine();
pstmt.setString(1, Rollno);
  System.out.print("\tName: ");
            String s_name= sc.nextLine();
pstmt.setString(2, s_name);
 System.out.print("\tClass: ");
            String S_class= sc.nextLine();
pstmt.setString(3, S_class);
   System.out.print("\tDivision: ");
            String Division= sc.nextLine();
pstmt.setString(4, Division);
  System.out.print("\tContact: ");
            String Contact= sc.nextLine();
pstmt.setString(5, Contact);
 int rows = pstmt.executeUpdate();
            System.out.println("\nRow(s) inserted sucessfully : "+ rows);
            System.out.println("----- ----- ----- -----");
  System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine();
 }
        catch (SQLException e) {e.printStackTrace();}

    } 
System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine(); }
        if (conn != null) {
            try {
conn.close();
sc.close();
System.exit(0);
            } catch (SQLException ex) {
ex.printStackTrace();
            }
        }
    }
        System.out.println("\n\n----- Update Book Details -----\n\n");
        PreparedStatement pstmt = null;
        String sql= "UPDATE book SET title = ?, author = ?, publication = ?, edition = ?, pub_year = ? WHERE id = ?";
   try {
            pstmt = conn.prepareStatement(sql);
sc.nextLine();
            System.out.print("Enter Book ID to update : ");
            String bookid= sc.nextLine();
pstmt.setString(6, bookid);
            String Author= sc.nextLine();
pstmt.setString(2, Author);
            System.out.print("\tPublication: ");
            String Publication= sc.nextLine();
pstmt.setString(3, Publication);
            System.out.print("\tPublication Year: ");
            String pub_year= sc.nextLine();

pstmt.setString(5, pub_year);
           int rows = pstmt.executeUpdate();
            System.out.println("\nRow(s) updated sucessfully : "+ rows);
            System.out.println("----- ----- ----- -----");
 }
        System.out.println("\n\n----- Update Student Details -----\n\n");
        System.out.println("Enter Student Details:");

        PreparedStatement pstmt = null;
        String sql= "UPDATE student SET s_name= ?, class = ?, division = ?, contact = ? WHERE rollno= ?";

            int rows = pstmt.executeUpdate();
            System.out.println("\nRow(s) updated sucessfully : "+ rows);
            System.out.println("----- ----- ----- -----");

            System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine();
    }
        catch (SQLException e) {e.printStackTrace();}
    }

            int rows = pstmt.executeUpdate();
if(rows == 0){
                System.out.println("\nFailed to delete a Book coz it is borrowed by a student.\nIn order to delete book student should return it.");
            }
else{
                System.out.println("\nRow(s) deleted sucessfully : "+ rows);
            }
            System.out.println("----- ----- ----- -----");
        }
        catch (SQLException e) {e.printStackTrace();}
      System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine();
    }
        System.out.println("\n\n----- Delete Student -----\n\n");
        PreparedStatement pstmt = null;
        String sql= "DELETE FROM student WHERE rollno= ?";
   try {
            pstmt = conn.prepareStatement(sql);
sc.nextLine();
            System.out.print("Enter Student's Roll No. : ");
            String rollno= sc.nextLine();
pstmt.setString(1, rollno);

            int rows = pstmt.executeUpdate();
            System.out.println("\nRow(s) deleted sucessfully : "+ rows);
            System.out.println("----- ----- ----- -----");
        catch (SQLException e) {
            System.out.println("\nFailed to delete a student coz student has borrowed book(s).\nIn order to delete a student, student should return borrowed book(s).");
    public static void getBook(Connection conn){
        System.out.print("\033[H\033[2J"); // ANSI escape code to clear the screen
        System.out.flush();
        System.out.println("\n\n----- Book Details -----\n\n");
        System.out.println("----- ------ ----- ----- ------ ----- ----- ------ ----- ----- ------ -----");
        System.out.println("ID\tTitle\tAuthor\tPublication\tEdition\tPublication Year\tBorrowedBy\tIssued Date\tStatus");
        System.out.println("----- ------ ----- ----- ------ ----- ----- ------ ----- ----- ------ -----");
 String sql = "SELECT * FROM book WHERE id = ?";
  try {
            PreparedStatement pstmt = conn.prepareStatement(sql);
            System.out.print("Enter Book Id : ");
            String id= sc.nextLine();
pstmt.setInt(1, Integer.parseInt(id));
ResultSetresultSet = pstmt.executeQuery();
            while (resultSet.next()) {
                int bookId = resultSet.getInt("id");
                String title = resultSet.getString("title");
                String author = resultSet.getString("author");
                String publication = resultSet.getString("publication");
                String edition = resultSet.getString("edition");
                int pub_year = resultSet.getInt("pub_year");
                int student_id = resultSet.getInt("student_id");
                Date issuedate = resultSet.getDate("issuedate");
                String stat = resultSet.getString("stat");
                System.out.print("\n" + bookId + "\t");
                System.out.print("" + title + "\t");
                System.out.print("" + author + "\t");
                System.out.print("" + publication + "\t");
                System.out.print("" + edition + "\t");
                System.out.print("" + pub_year + "\t");
                System.out.print("" + student_id + "\t");
                System.out.print("" + issuedate + "\t");
                System.out.print("" + stat + "\t");
            }
        } catch (SQLException e) {e.printStackTrace();}

        System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine();
    }
                System.out.print("\n" + rollno + "\t");
                System.out.print("" + s_name + "\t");
                System.out.print("" + s_class + "\t");
                System.out.print("" + division + "\t");
                System.out.print("" + contact + "\t");
            }
        } catch (SQLException e) {e.printStackTrace();}

        System.out.println("\n\nPress 'Enter' key to return to main menu....");
sc.nextLine();




Back-end Code:

CREATE TABLE `book` (
  `id` int NOT NULL AUTO_INCREMENT,
  `title` varchar(255) DEFAULT NULL,
  `author` varchar(255) DEFAULT NULL,
  `publication` varchar(255) DEFAULT NULL,
  `edition` varchar(255) DEFAULT NULL,
  `pub_year` int DEFAULT NULL,
  `student_id` int DEFAULT NULL,
  `issuedate` date DEFAULT NULL,
  `stat` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`),
  KEY `student_id` (`student_id`)

CREATE TABLE `student` (
  `rollno` int NOT NULL,
  `s_name` varchar(255) NOT NULL,
  `class` varchar(255) NOT NULL,
  `division` varchar(255) NOT NULL,
  `contact` varchar(255) NOT NULL,
  PRIMARY KEY (`rollno`)
)
