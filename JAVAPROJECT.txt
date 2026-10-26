import java.util.ArrayList;
import java.util.Scanner;

class Participant {
    private int id;
    private String name;
    private String email;
    private String eventName;

    public Participant(int id, String name, String email, String eventName) {
        this.id = id;
        this.name = name;
        this.email = email;
        this.eventName = eventName;
    }

    public void display() {
        System.out.println("ID: " + id);
        System.out.println("Name: " + name);
        System.out.println("Email: " + email);
        System.out.println("Event: " + eventName);
        System.out.println("----------------------");
    }
}

class ParticipantService {
    private ArrayList<Participant> list = new ArrayList<>();

    public void addParticipant(Participant p) {
        list.add(p);
        System.out.println("Participant Registered Successfully!");
    }

    public void showParticipants() {
        System.out.println("\n--- Participant List ---");

        if (list.isEmpty()) {
            System.out.println("No participants registered.");
            return;
        }

        for (Participant p : list) {
            p.display();
        }
    }
}

public class MainApp {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ParticipantService service = new ParticipantService();

        int id = 1;
        int choice;

        do {
            System.out.println("\n================================");
            System.out.println(" EVENT REGISTRATION SYSTEM");
            System.out.println("================================");
            System.out.println("1. Register Participant");
            System.out.println("2. Display Participants");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");

            while (!sc.hasNextInt()) {
                System.out.println("Please enter a valid number.");
                sc.next();
                System.out.print("Enter your choice: ");
            }

            choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {
                case 1:
                    System.out.print("Enter participant name: ");
                    String name = sc.nextLine();

                    System.out.print("Enter email: ");
                    String email = sc.nextLine();

                    System.out.print("Enter event name: ");
                    String eventName = sc.nextLine();

                    if (name.trim().isEmpty()
                            || email.trim().isEmpty()
                            || eventName.trim().isEmpty()) {
                        System.out.println("Error: All fields are required.");
                        break;
                    }

                    Participant p = new Participant(
                            id++, name, email, eventName
                    );

                    service.addParticipant(p);
                    break;

                case 2:
                    service.showParticipants();
                    break;

                case 3:
                    System.out.println("Thank you for using the system!");
                    break;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }

        } while (choice != 3);

        sc.close();
    }
}