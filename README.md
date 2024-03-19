# -GroceryCRSystem
import java.util.ArrayList;
import java.util.Scanner;

class Feedback {
    int id;
    String customerName;
    String details;
    String type; // Complaint or Suggestion
    String status; // Pending, In Progress, Resolved

    public Feedback(int id, String customerName, String details, String type, String status) {
        this.id = id;
        this.customerName = customerName;
        this.details = details;
        this.type = type;
        this.status = status;
    }

    @Override
    public String toString() {
        return "Feedback ID: " + id + ", Customer: " + customerName + ", Type: " + type + 
               ", Status: " + status + ", Details: " + details;
    }
}

public class GroceryCRSystem {
    private static ArrayList<Feedback> feedbackList = new ArrayList<>();
    private static int feedbackCount = 0;
    private static Scanner scanner = new Scanner(System.in);

    public static void addFeedback() {
        System.out.println("Enter customer name:");
        String name = scanner.nextLine();
        System.out.println("Enter feedback details:");
        String details = scanner.nextLine();
        System.out.println("Is this a complaint or a suggestion? (C/S)");
        String type = scanner.nextLine().equalsIgnoreCase("C") ? "Complaint" : "Suggestion";

        Feedback feedback = new Feedback(++feedbackCount, name, details, type, "Pending");
        feedbackList.add(feedback);
        System.out.println("Feedback added successfully.");
    }

    public static void updateFeedbackStatus() {
        System.out.println("Enter feedback ID:");
        int id = Integer.parseInt(scanner.nextLine()); // Changed to use nextLine() and then parse
        System.out.println("Enter new status (Pending, In Progress, Resolved):");
        String status = scanner.nextLine();

        for (Feedback feedback : feedbackList) {
            if (feedback.id == id) {
                feedback.status = status;
                System.out.println("Feedback status updated.");
                return;
            }
        }
        System.out.println("Feedback ID not found.");
    }

    public static void listFeedbacks() {
        for (Feedback feedback : feedbackList) {
            System.out.println(feedback);
        }
    }

    public static void main(String[] args) {
        while (true) {
            System.out.println("\n1. Add Feedback\n2. Update Feedback Status\n3. List Feedbacks\n4. Exit");
            int choice = Integer.parseInt(scanner.nextLine()); // Changed to use nextLine() and then parse
            switch (choice) {
                case 1:
                    addFeedback();
                    break;
                case 2:
                    updateFeedbackStatus();
                    break;
                case 3:
                    listFeedbacks();
                    break;
                case 4:
                    System.exit(0);
                default:
                    System.out.println("Invalid option, please try again.");
            }
        }
    }
}
