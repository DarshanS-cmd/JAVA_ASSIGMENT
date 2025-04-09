package librarymangement;

import java.sql.*;
import java.util.Scanner;

public class LibraryMangement {
    private static final String URL = "jdbc:mysql://localhost:3306/db1";
    private static final String USER = "root";
    private static final String PASSWORD = "Darshan@09";

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            System.err.println("Error: MySQL JDBC Driver not found.");
            e.printStackTrace();
            return;
        }

        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD)) {
            while (true) {
                System.out.println("\nLibrary Management System - CRUD Operations");
                System.out.println("1. Add a Book");
                System.out.println("2. View All Books");
                System.out.println("3. Update Book Details");
                System.out.println("4. Delete a Book");
                System.out.println("5. Exit");
                System.out.print("Choose an option: ");

                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        addBook(conn, scanner);
                        break;
                    case 2:
                        viewBooks(conn);
                        break;
                    case 3:
                        updateBook(conn, scanner);
                        break;
                    case 4:
                        deleteBook(conn, scanner);
                        break;
                    case 5:
                        System.out.println("Exiting...");
                        return;
                    default:
                        System.out.println("Invalid choice. Please try again.");
                }
            }
        } catch (SQLException e) {
            System.err.println("Database connection error:");
            e.printStackTrace();
        }
    }

    // CREATE: Add a book
    private static void addBook(Connection conn, Scanner scanner) throws SQLException {
        System.out.print("Enter book title: ");
        String title = scanner.nextLine();
        System.out.print("Enter genre: ");
        String genre = scanner.nextLine();
        System.out.print("Enter published year: ");
        int publishedYear = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        String query = "INSERT INTO book (title, genre, published_year) VALUES (?, ?, ?)";
        try (PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setString(1, title);
            pstmt.setString(2, genre);
            pstmt.setInt(3, publishedYear);
            pstmt.executeUpdate();
            System.out.println("Book added successfully!");
        }
    }

    // READ: View all books
    private static void viewBooks(Connection conn) throws SQLException {
        String query = "SELECT * FROM book";
        try (Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery(query)) {

            System.out.println("\nBooks in Library:");
            while (rs.next()) {
                System.out.println("Book ID: " + rs.getInt("book_id"));
                System.out.println("Title: " + rs.getString("title"));
                System.out.println("Genre: " + rs.getString("genre"));
                System.out.println("Published Year: " + rs.getInt("published_year"));
                System.out.println("-----------------------------");
            }
        }
    }

    // UPDATE: Modify book details
    private static void updateBook(Connection conn, Scanner scanner) throws SQLException {
        System.out.print("Enter book ID to update: ");
        int bookId = scanner.nextInt();
        scanner.nextLine(); // Consume newline
        System.out.print("Enter new title: ");
        String title = scanner.nextLine();
        System.out.print("Enter new genre: ");
        String genre = scanner.nextLine();
        System.out.print("Enter new published year: ");
        int publishedYear = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        String query = "UPDATE book SET title=?, genre=?, published_year=? WHERE book_id=?";
        try (PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setString(1, title);
            pstmt.setString(2, genre);
            pstmt.setInt(3, publishedYear);
            pstmt.setInt(4, bookId);
            int rowsAffected = pstmt.executeUpdate();
            if (rowsAffected > 0) {
                System.out.println("Book updated successfully!");
            } else {
                System.out.println("No book found with the given ID.");
            }
        }
    }

    // DELETE: Remove a book
    private static void deleteBook(Connection conn, Scanner scanner) throws SQLException {
        System.out.print("Enter book ID to delete: ");
        int bookId = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        String query = "DELETE FROM book WHERE book_id=?";
        try (PreparedStatement pstmt = conn.prepareStatement(query)) {
            pstmt.setInt(1, bookId);
            int rowsAffected = pstmt.executeUpdate();
            if (rowsAffected > 0) {
                System.out.println("Book deleted successfully!");
            } else {
                System.out.println("No book found with the given ID.");
            }
        }
    }
}
