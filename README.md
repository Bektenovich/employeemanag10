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

### 3. **Graphical User Interface with User-Friendly Design**

The **Graphical User Interface (GUI)** is designed to be:
- **Intuitive**: Easy to navigate through the available movies, showtimes, and ticket booking process.
- **Aesthetic**: Clean design with clear labels and buttons.
- **Efficient**: Ensures that users can quickly make selections and complete the booking process without confusion.

#### Key Features:
- **Movie Selection Interface**: Allows users to easily select a movie.
- **Booking Interface**: Provides input fields for selecting the number of tickets and completing the booking process.
- **Clear Navigation**: Labels and buttons are intuitively placed for easy understanding.

#### Example Code for GUI Design:
```java
public class MovieBookingView extends Application {
    @Override
    public void start(Stage primaryStage) {
        // Create a button for booking tickets
        Button bookButton = new Button("Book Ticket");
        bookButton.setOnAction(event -> handleBooking());

        // Table to display available movies
        TableView<Movie> movieTable = new TableView<>();
        movieTable.setItems(getMovies());  // Fetch movies from the model
        
        // Set up the layout for the UI
        VBox layout = new VBox(movieTable, bookButton);
        Scene scene = new Scene(layout);
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void handleBooking() {
        // Logic for booking the ticket
    }
}
```
### 4. **Responsive Design**

The **Responsive Design** ensures the application adapts to various screen sizes:
- **Flexible Layout**: GUI elements automatically resize or reorganize based on the screen size or window adjustments.
- **Cross-Device Compatibility**: The interface remains usable on desktops, tablets, and mobile devices, ensuring a seamless experience across different devices.

#### Key Features:
- **Adapts to Different Screen Sizes**: The layout will adjust elements based on the user's device screen size.
- **Mobile-Friendly Design**: When used on smaller devices like smartphones, the application should display with legible text and buttons without horizontal scrolling.

#### Example Code for Responsive Layout:
```java
VBox layout = new VBox();
layout.setSpacing(10);  // Adjustable spacing between elements

HBox buttonsLayout = new HBox();
buttonsLayout.setAlignment(Pos.CENTER);
buttonsLayout.setSpacing(20);

layout.getChildren().addAll(movieTable, buttonsLayout, bookButton);
```
### 5. **Message Notifications for Exceptions in Case of Wrong User Inputs**

The system provides **error messages** when users input invalid data:
- **Booking Error**: If a user tries to book more tickets than are available, an error message is displayed: *"Not enough seats available."*
- **Input Validation**: If the user enters incorrect data (e.g., text where a number is expected), the system will display an error message.

#### Key Features:
- **Error Handling**: Whenever an error occurs, users are notified with a clear and helpful message.
- **Exception Management**: Different types of errors (e.g., invalid input or booking failure) are captured and displayed with appropriate messages.

#### Example of Exception Handling Code:
```java
private void handleBooking() {
    try {
        // Attempt to book the tickets
        bookingService.bookTicket(movie, seats);
    } catch (BookingException e) {
        showError("Booking Error: " + e.getMessage());
    }
}

private void showError(String message) {
    Alert alert = new Alert(AlertType.ERROR);
    alert.setTitle("Error");
    alert.setHeaderText(null);
    alert.setContentText(message);
    alert.showAndWait();
}
```
### 6. **Controller**

The **Controller** acts as an intermediary between the **Model** and **View**:
- **Handles User Input**: It processes user actions, such as selecting a movie or booking tickets.
- **Interacts with the Model**: It updates the model based on the user's choices (e.g., booking a ticket).
- **Updates the View**: After processing the input, it updates the view (e.g., updating available seats after a booking).

#### Key Features:
- **Event Handling**: The controller listens for user events (such as clicks on buttons) and invokes corresponding methods to update the model or view.
- **User Interaction**: Ensures that user inputs (like booking a ticket) are passed to the model and that the view is updated with the results.
- **Separation of Concerns**: Ensures the business logic (model) and UI logic (view) are separate, making the codebase cleaner and easier to maintain.

#### Example of Controller Code:
```java
public class MovieBookingController {
    private MovieBookingView view;
    private MovieBookingModel model;

    public MovieBookingController(MovieBookingView view, MovieBookingModel model) {
        this.view = view;
        this.model = model;
    }

    // Method to handle booking tickets
    public void handleBooking(Movie movie, int seats) {
        // Handle booking process by calling the model
        model.bookMovie(movie, seats);
        // Update the view with the new available seats
        view.updateAvailableSeats(movie.getSessionTime());
    }
}
```
### 7. **Unit Testing**

**Unit Testing** is essential to ensure that the model's methods work correctly:
- Tests focus on validating the business logic, such as ticket price calculation, seat availability, etc.
- Unit tests verify that the model behaves as expected under various conditions, and that the application continues to function properly as new features are added or changes are made.

#### Key Features:
- **Test Coverage**: Unit tests ensure the correctness of core functionality, such as calculating ticket prices, validating user input, and checking seat availability.
- **Reliability**: Helps ensure that the application behaves as expected under various scenarios, improving its overall stability and reliability.
- **Regression Testing**: Prevents the introduction of bugs when adding new features or making updates by ensuring that existing features still work correctly.

#### Example of Unit Test:
```java
import static org.junit.jupiter.api.Assertions.assertEquals;

public class BookingTest {
    @Test
    public void testCalculateTotalPrice() {
        // Arrange: Create a movie object with a title and description
        Movie movie = new Movie("Movie Title", "Description", LocalDateTime.now());
        
        // Create a booking with 3 tickets
        Booking booking = new Booking(movie, 3);
        
        // The price per ticket is 10.0, so the expected total price is 30.0
        double expectedPrice = 30.0;  
        
        // Act & Assert: Verify that the calculated price matches the expected price
        assertEquals(expectedPrice, booking.calculateTotalPrice(), "Total price calculation is incorrect.");
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

