import java.util.Scanner;

class Flight {
    private String flightNumber;
    private String source;
    private String destination;
    private int seatsAvailable;

    public Flight(String flightNumber, String source, String destination, int seatsAvailable) {
        this.flightNumber = flightNumber;
        this.source = source;
        this.destination = destination;
        this.seatsAvailable = seatsAvailable;
    }

    public String getFlightNumber() {
        return flightNumber;
    }

    public String getSource() {
        return source;
    }

    public String getDestination() {
        return destination;
    }

    public int getSeatsAvailable() {
        return seatsAvailable;
    }

    public void reserveSeats(int numSeats) {
        if (numSeats <= seatsAvailable) {
            seatsAvailable -= numSeats;
            System.out.println("Seats reserved successfully!");
        } else {
            System.out.println("Sorry, seats not available.");
        }
    }
}

public class AirlineReservationSystem {
    private Flight[] flights;

    public AirlineReservationSystem() {
        // Initialize flights
        flights = new Flight[3];
        flights[0] = new Flight("F001", "New York", "London", 200);
        flights[1] = new Flight("F002", "Tokyo", "Paris", 150);
        flights[2] = new Flight("F003", "Sydney", "Dubai", 100);
    }

    public void displayFlights() {
        System.out.println("Available flights:");
        for (Flight flight : flights) {
            System.out.println("Flight Number: " + flight.getFlightNumber());
            System.out.println("Source: " + flight.getSource());
            System.out.println("Destination: " + flight.getDestination());
            System.out.println("Seats Available: " + flight.getSeatsAvailable());
            System.out.println();
        }
    }

    public void reserveSeats(String flightNumber, int numSeats) {
        Flight selectedFlight = null;
        for (Flight flight : flights) {
            if (flight.getFlightNumber().equals(flightNumber)) {
                selectedFlight = flight;
                break;
            }
        }

        if (selectedFlight != null) {
            selectedFlight.reserveSeats(numSeats);
        } else {
            System.out.println("Invalid flight number.");
        }
    }

    public static void main(String[] args) {
        AirlineReservationSystem airlineReservationSystem = new AirlineReservationSystem();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. Display available flights");
            System.out.println("2. Reserve seats");
            System.out.println("3. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    airlineReservationSystem.displayFlights();
                    break;
                case 2:
                    System.out.print("Enter flight number: ");
                    String flightNumber = scanner.next();
                    System.out.print("Enter number of seats to reserve: ");
                    int numSeats = scanner.nextInt();
                    airlineReservationSystem.reserveSeats(flightNumber, numSeats);
                    break;
                case 3:
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
            }

            System.out.println();
        }
    }
}
