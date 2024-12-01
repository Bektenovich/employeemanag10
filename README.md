# Movie Ticket Booking System

## Description

The Movie Ticket Booking System allows users to select movies, book seats for sessions, and pay for tickets online. The application provides an intuitive interface for easily searching for movies, selecting session times, and reviewing booking history. It also allows administrators to manage movies, sessions, and bookings.

## Project Requirements

1. Users can view a list of available movies.
2. Ability to choose sessions and times.
3. Seat booking in the cinema.
4. Payment for tickets through various methods (e.g., credit card).
5. User registration and login.
6. Administrator can add, edit, and delete movies.
7. Manage sessions for each movie.
8. Generation of an electronic ticket after successful booking.
9. View booking history.
10. Notifications for booking confirmation and updates.


# Movie Ticket Booking System

## Project Overview

The **Movie Ticket Booking System** is a Java application that allows users to view movies, select showtimes, and book tickets. The system follows the **Model-View-Controller (MVC)** design pattern, separating the application into three main components: **Model**, **View**, and **Controller**. This structure promotes code organization and simplifies testing and maintenance.

---

## Model-View-Controller (MVC) Design Pattern

### 1. **Model**

**Model** represents the data and business logic of the application. It contains classes for handling data such as movies, bookings, users, and pricing. The model also includes the logic for booking tickets, checking availability, and calculating total prices.

#### Responsibilities of the Model:
- **Data Classes**: Represent information about movies, bookings, users, and ticket prices.
- **Business Logic**: Implement the logic to calculate prices, check seat availability, and manage the booking process.
- **Data Management**: Functions to add, remove, and update data (e.g., adding a movie, removing a booking).

#### Example of Model Code:
```java
public class Movie {
    private String title;
    private String description;
    private LocalDateTime sessionTime;

    // Constructors, getters, setters
    
    public boolean isAvailable() {
        // Business logic to check movie availability
    }
}

public class Booking {
    private Movie movie;
    private int seatsBooked;
    
    public double calculateTotalPrice() {
        // Logic to calculate total price based on movie and number of seats
    }
}
```
### 2. **View**

The **View** handles the graphical user interface (GUI), which allows users to interact with the application. The system uses **JavaFX** to display the available movies, their sessions, and booking details.

#### Key Features of the View:
- **Movie Selection**: Users can view the available movies and select a session.
- **Booking Interface**: Users can choose the number of tickets and proceed with booking.
- **Responsive Design**: The interface adapts to various screen sizes to ensure it is usable on desktops, tablets, and mobile devices.

#### Example of View Code:
```java
public class MovieBookingView extends Application {
    @Override
    public void start(Stage primaryStage) {
        // Create GUI components like buttons and input fields
        Button bookButton = new Button("Book Ticket");
        bookButton.setOnAction(event -> handleBooking());

        // Table to display available movies
        TableView<Movie> movieTable = new TableView<>();
        movieTable.setItems(getMovies());  // Fetch movies from the model
        
        // Layout for the UI
        VBox layout = new VBox(movieTable, bookButton);
        Scene scene = new Scene(layout);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void handleBooking() {
        // Logic to handle booking action
    }
}
```

## Team Members
- Bekten uly Mukhammed (Tester)
- Rahmatova Leyla (Developer)
- Kokumova Aidana (Designer and Frontend Developer)

## Roles of Group Members
- Bekten uly Mukhammed: Functional testing,presentation and interface validation.
- Rahmatova Leyla: Development of server-side logic and payment API integration.
- Kokumova Aidana: Development of the user interface using JavaFX and pgAdmin.

## Screenshots

![Movie Selection Screen](https://example.com/film-selection.png)
*Movie selection screen.*

![Booking Screen](https://example.com/booking-screen.png)
*Seat booking and ticket payment screen.*

## UML Class Diagram

![UML Class Diagram](https://example.com/uml-class-diagram.png)
*Class diagram of the Movie Ticket Booking System.*

## Media content

Video and presentation is available at [Google Docs link](https://docs.google.com/your-link).

